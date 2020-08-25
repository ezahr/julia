# julia 

````
##################################################################
# Purpose: Procedure to clone de github repo on your pc
# Arguments:
# Return:
##################################################################

## https git clone https://ezahr:Peter\!....github.com/ezahr/fail-fast-and-cheap.git
## ssh   git clone https://github.com/ezahr/fail-fast-and-cheap.git
##       http://gitlab.example.com/root/ezahr_julia.git


SCRIPT_DIR=/home/boscp08/Projects/scratch/virtual-insanity/fail-fast-and-cheap
GITHUB_PROJECT_DIR=/home/boscp08/Projects/scratch/virtual-insanity/
GITLAB_PROJECT_DIR=/home/boscp08/Projects/gitlab.example.com/
REPO=julia
JOB_START_DATE_TIME=`date +%Y%m%d_%H_%M`

git_clone() {
 
 cd ${GITHUB_PROJECT_DIR}
 rm -rf ${REPO}
 git clone https://github.com/ezahr/${REPO}.git


 cd ${GITLAB_PROJECT_DIR}
 rm -rf ${REPO}
 git clone http://gitlab.example.com/root/${REPO}.git

cd $SCRIPT_DIR

# rsync -av --exclude=".*" src dest 

rsync -av --exclude=".*"  ${GITHUB_PROJECT_DIR}/${REPO}  ${GITLAB_PROJECT_DIR}  #maakt em eveentueel aan. 
# 
# cd ${GITLAB_PROJECT_DIR}/${REPO} 
# 
git add .
# git status
git commit -m `date +%Y%m%d_%H_%M`
# git status
git push origin master


}
````
