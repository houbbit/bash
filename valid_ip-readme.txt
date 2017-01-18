 This script is originally written by Mitch Frazier.
 
 If you save this script as "valid_ip.sh" and then run it directly it will run some tests and prints the results:

  # sh valid_ip.sh
  4.2.2.2             : good
  a.b.c.d             : bad
  192.168.1.1         : good
  0.0.0.0             : good
  255.255.255.255     : good
  255.255.255.256     : bad
  192.168.0.1         : good
  192.168.0           : bad
  1234.123.123.123    : bad

In the function valid_ip, the if statement uses a regular expression to make sure the subject IP address consists of four dot separated numbers:

  if [[ $ip =~ ^[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}$ ]]; then

If that test passes then the code inside the if statement separates the subject IP address into four parts at the dots and places the parts in an array:

  OIFS=$IFS
  IFS='.'
  ip=($ip)
  IFS=$OIFS

It does this by momentarily changing bash's Internal Field Separator variable so that rather than parsing words as whitespace separated items, bash parses them as dot separated. Putting the value of the subject IP address inside parenthesis and assigning it to itself thereby turns it into an array where each dot separated number is assigned to an array slot. Now the individual pieces are tested to make sure they're all less than or equal to 255 and the status of the test is saved so that it can be returned to the caller:

  [[ ${ip[0]} -le 255 && ${ip[1]} -le 255 \
          && ${ip[2]} -le 255 && ${ip[3]} -le 255 ]]
  stat=$?

Note that there's no need to test that the numbers are greater than or equal to zero because the regular expression test has already eliminated any thing that doesn't consist of only dots and digits.
