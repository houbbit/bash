Create new ff-profile based on a preconfigured profile.

Setup:
- execute 'firefox -p'
- create new profile, install desired addons, configure desired proxies, configure optional server certificates, add desired skin
- locate profile in /home/user/.mozilla/firefox/ and copy the profile direcory name.
- configure profile directory in $DEFAULT_PROF_PATH and main firefox path in FIREFOX_PROF_PATH

Execute:
ff-newprofile blup
after that run the profile:
firefox -p blup
