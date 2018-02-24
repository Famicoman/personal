# archivebotjr

I was able to make a slackbot usable for archiving, https://famicoman.com/2016/02/29/rtmbot-archivebotjr-a-slack-bot-for-archiving/

Here is the repo, https://github.com/Famicoman/rtmbot-archivebotjr

## Notes

* ~~python-rtmbot - https://github.com/slackhq/python-rtmbot~~
* python-rtmbot - https://github.com/slackapi/python-rtmbot
* Compiling ffmpeg on Debian - https://trac.ffmpeg.org/wiki/CompilationGuide/Ubuntu
* youtube-dl - https://github.com/rg3/youtube-dl/

```youtube-dl --prefer-ffmpeg --ffmpeg-location /home/slackbot/bin --title --continue --retries 4 --write-info-json --write-description --write-thumbnail --write-annotations --all-subs --ignore-errors -f bestvideo+bestaudio```