# show tag

    git tag
    git show v0.1
# create tag

    git tag -a v0.1 -m "jgirls001 version 0.1, show posts, no links yet"

# push tag
By default, the git push command doesn’t transfer tags to remote servers. You will have to explicitly push tags to a shared server after you have created them.
https://git-scm.com/book/en/v2/Git-Basics-Tagging

    git push origin v0.1

# Push without asking for user/pass,  git@github.com:twoutlook/jgirls001.git
http://stackoverflow.com/questions/5813726/troubleshooting-git-push-it-asks-for-a-user-pass

BASED ON DEFAULT

`git remote add origin https://github.com/twoutlook/jgirls001.git` 

ADD ONE MORE

`git remote set-url origin git@github.com:twoutlook/jgirls001.git`

# auto deploy
http://stackoverflow.com/questions/7303518/automatically-deploy-from-github-to-server-on-push
https://github.com/logsol/Github-Auto-Deploy
http://www.thisprogrammingthing.com/2013/automatically-updating-your-website-using-githubs-service-hooks/
