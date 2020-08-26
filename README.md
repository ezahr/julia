# julia menu gestuurd



````
#! /bin/bash
# //////////////////////////////////////////////////////////////////////////////////////////
# File Type   : BASH Script (needs GIT-CLI  installed  ).
# https git clone https://${1}:Peter\!....github.com/${1}/fail-fast-and-cheap.git
# ssh   git clone https://github.com/${1}/fail-fast-and-cheap.git
# //////////////////////////////////////////////////////////////////////////////////////////



# define your feedback here


MENU=true

SCRIPT_DIR=/home/boscp08/Projects/scratch/virtual-insanity/fail-fast-and-cheap
GITHUB_PROJECT_DIR=/home/boscp08/Projects/scratch/virtual-insanity/
GITLAB_PROJECT_DIR=/home/boscp08/Projects/gitlab.example.com/
GITLAB_PROJECT_DIR_PI8GB=/home/boscp08/Projects/gitlab.example.com/pi8gb/


enter_cont() {
    echo
    echo
    echo -n "Press enter to Continue"
    read
}


##################################################################
# Purpose: Procedure to clone de github repo on your pc
# Arguments:
# Return:
##################################################################

git_clone() {

 # echo "Running:"${FUNCNAME[0]}" $@

 arg1=${1} #${USER}
 arg2=${2} #${REPO}

 #echo "cd  ${GITHUB_PROJECT_DIR}"
 
 cd ${GITHUB_PROJECT_DIR}
 pwd
 rm -rf ${2}
 git clone https://github.com/${1}/${2}.git


 #echo  "cd ${GITLAB_PROJECT_DIR}"
 
 cd ${GITLAB_PROJECT_DIR}
 pwd
 rm -rf ${2}
 git clone http://gitlab.example.com/root/${2}.git
 
 # rsync -av --exclude=".*" src dest 
rsync -av --exclude=".*"  ${GITHUB_PROJECT_DIR}${2} ${GITLAB_PROJECT_DIR}  #maakt em eveentueel aan. 

cd ${GITLAB_PROJECT_DIR}${2}
 git add .
 # git status
 git commit -m `date +%Y%m%d_%H_%M`
# # git status
 git push origin master
 cd $SCRIPT_DIR

#---
echo "------------"
 cd ${GITLAB_PROJECT_DIR_PI8GB}
 rm -rf ${2}
 git clone http://192.168.2.11/root/${2}.git
# #git clone git@192.168.2.11:root/$1.git
 rsync -av --exclude=".*"  ${GITHUB_PROJECT_DIR}${2}  ${GITLAB_PROJECT_DIR_PI8GB}  #maakt em eveentueel aan. 
 cd ${GITLAB_PROJECT_DIR_PI8GB}${2}
 git add .
# # git status
 git commit -m `date +%Y%m%d_%H_%M`
# # git status
 git push origin master
# 
cd $SCRIPT_DIR

echo "  "
echo "hope the run will be okay."
enter_cont

}


##################################################################
# Purpose: show main menu
# Arguments:
# Return:
##################################################################
show_main_menu(){
clear
# A menu driven shell script
#"A menu is nothing but a list of commands presented to a user by a shell script"

# ----------------------------------
# Step: User defined function  10 20 30 ( 40 50)
# ----------------------------------
pause(){
  read -p "Press [Enter] key to continue..." fackEnterKey
}
# function to display menus
show_menus() {
  echo "~~~~~~~~~~~~~~~~~~~~~"
  echo " M A I N - M E N U  "
  echo "~~~~~~~~~~~~~~~~~~~~~"
  echo "~~~~~~~~~~~~~~~~~~~~~"
  echo "10. git_clone ezahr julia                                   "
  echo "11. git_clone OCI                                           "
  echo "12  show_parameters                                         "
  echo "20. set_all_Dockerfiles   $CERT_HOST_IP                     "
  echo "21. set_docker_compose_travis_yml_without_volumes           "
  echo "22. set_Dockerfile_mock_nlx                                 "
  echo "23. set_Dockerfile_clerk_frontend_without_volumes           "
  echo "24. set_Dockerfile_waardepapieren_service_without_volumes   "
  echo "25. set_clerk_frontend_nginx_conf                           "
  echo "26. set_waardepapieren_service_config_compose_travis_json    "
  echo "~~~~~~~~~~~~~~~~~~~~~"
  echo "99. Exit"
}
# read input from the keyboard and take a action
# invoke the one() when the user select 1 from the menu option.
# invoke the two() when the user select 2 from the menu option.
# Exit when user the user select 100 form the menu option.

read_options(){
	local choice
	read -p "Enter choice [ 1 - 99] " choice
	case $choice in
        10) git_clone ezahr julia                                                  ;;
        11) git_clone OCI                                                          ;;
        12) show_parameters                                                        ;;
        20) set_all_Dockerfiles                                                    ;;
        21) set_docker_compose_travis_yml_without_volumes                          ;;
        22) set_Dockerfile_mock_nlx                                                ;;
        23) set_Dockerfile_clerk_frontend_without_volumes                          ;;
        24) set_Dockerfile_waardepapieren_service_without_volumes                  ;;
        25) set_clerk_frontend_nginx_conf                                          ;;
        26) set_waardepapieren_service_config_compose_travis_json                  ;;
        99) Exit                                                                   ;;
		*) echo -e "${RED}Error...${STD}" && sleep 1
	esac
}

# ----------------------------------------------
# Step #3: Trap CTRL+C, CTRL+Z and quit singles
# ----------------------------------------------
#trap '' SIGINT SIGQUIT SIGTSTP

# -----------------------------------
# Step #4: Main logic - infinite loop
# ------------------------------------
while true
do
	show_menus
	read_options
done
}


#######################
## M A I N
# program starts here actually
#######################

echo "***"
echo "***  Welcome to a `uname` gitsync"
echo "***"
echo "*** SCRIPT_DIR = $SCRIPT_DIR                             "   #=/home/boscp08/Projects/scratch/virtual-insanity/fail-fast-and-cheap
echo "*** GITHUB_PROJECT_DIR= $GITHUB_PROJECT_DIR              "   #=/home/boscp08/Projects/scratch/virtual-insanity/
echo "*** GITLAB_PROJECT_DIR= $GITLAB_PROJECT_DIR              "   #=/home/boscp08/Projects/gitlab.example.com/
echo "*** GITLAB_PROJECT_DIR_PI8GB= $GITLAB_PROJECT_DIR_PI8GB  "   #=/home/boscp08/Projects/gitlab.example.com/pi8gb/

enter_cont


if [ ${MENU} = true ]
 then
clear
while true; do
    read -p "goto MAIN-MENU (y or n)" yn
    case $yn in
          [Yy]* ) show_main_menu ; break;;
          [Nn]* ) echo "N";  break;;
        * ) echo "Please answer yes or no.";;
    esac
done
fi



# eof 
````


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
