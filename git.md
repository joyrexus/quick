Git
===

Create a new repo.

    cd REPO
    git init
    git add .
    git commit -m 'initial commit'
    curl -u 'joyrexus' https://api.github.com/user/repos -d '{"name":"REPO"}'
    git remote add origin https://github.com/joyrexus/REPO.git
    git push -u origin master

