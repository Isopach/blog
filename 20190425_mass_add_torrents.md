# Mass Adding Torrent files to rTorrent

So you've been inactive for a while, or your computer died, or your server got nuked for whatever reason and you want to add your 10,000 torrent files to rTorrent... no problem!

## Steps     
1. Download all your torrent files as a zip (most trackers should offer this)
1. Transfer it to your server `scp -P 22 root@server.example.com:~/downloads/watch_directory`
1. SSH into your server `ssh root@server.example.com` and specify your password (I recommend using public_key instead)
1. Flatten your directory if needed. `cd ~/downloads/watch_directory` then `find . -mindepth 2 -type f -exec mv -t . -i '{}' +`
1. Specify the path to your watch directory by  `vi ~/.rtorrent.rc` and edit the line that starts with `schedule`, like this:     
`schedule = watch_directory_2,5,5,"load.normal=~/downloads/watch_directory/*.torrent"`     
Use `load.normal` to add torrents in a paused state, and `load.start` to automatically start torrents
1. Restart your rtorrent
1. Done!



###### References     
https://github.com/rakshasa/rtorrent/wiki/TORRENT-Watch-directories
https://www.reddit.com/r/seedboxes/comments/3mdfi3/adding_torrents_to_rtorrents_watch_folder_in_a/
