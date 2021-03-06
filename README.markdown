Use to only analyze *your* personal Quora account. Read [Quora's TOS](http://www.quora.com/about/tos).

Need to be running Ruby 1.8.7 with Firefox 3.6. I have only tested code under OS X Snow Leopard.

You'll also need [Firefox 3.6](http://www.mozilla.com/en-US/firefox/all-older.html) and the [JSSH Firefox Extenstion](http://wiki.openqa.org/display/WTR/FireWatir+Installation#FireWatirInstallation-2%29InstalltheJSSHFirefoxExtension) which you must install.

Before you begin crawling data, you'll need to start Firefox with the JSSH flag enabled. For OS X it will look like: /Applications/Firefox.app/Contents/MacOS/firefox-bin -jssh

---

If you're new to Ruby, do the following:

Install the right version of Ruby by opening a Terminal and typing:
curl -s https://rvm.beginrescueend.com/install/rvm -o rvm-installer ; chmod +x rvm-installer ; rvm_bin_path=~/.rvm/bin rvm_man_path=~/.rvm/share/man ./rvm-installer

Read the output of the script and follow the instructions it gives - it'll ask you to put a line into your .bashrc or similar file. Then log out of your terminal and open a new one, and run:
rvm install 1.8.7
rvm use 1.8.7

and then run
sudo gem update --system
and
sudo gem install bundler

You may need to run each of these and then run them again for it to work.

--

Clone this repository:
git clone git://github.com/stormy/Quora-Personal-Analytics.git

Run 'bundle install' and you should be set.

Log into Quora, otherwise, you won't get far.

Grab all your personal data as HTML files: 
ruby QuoraCrawler.rb "firstname-lastname"
(note: http://quora.com/*firstname-lastname*/. You might need a number like firstname-lastname-1).

Process your data:
ruby QuoraStats.rb "firstname-lastname"

Done. Example output: https://gist.github.com/1075650

Note: 'ruby QuoraCrawler.rb -h' and 'ruby QuoraStats.rb -h' will give you all the flags if you just want to process specifics.

--

Right now QuoraStats.rb is only outputting limited detail, but if you call the load_all_data method on a QuoraUser object in irb, you can play around with extracting out all the data that interests you.

Example:

user = QuoraUser.new('firstname-lastname')
user.load_all_data
user.answers[0].content.text.length => user's most recent answer's answer length
user.answers[0].voters[0].fullname => Full name of first person who upvoted users most recent answer)

