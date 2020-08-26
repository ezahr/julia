# julia main menu



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
  echo "20. ezahr AZ_ACI_waardepapieren-demo_westeurope_azurecontainer_io"
  echo "21. ezahr chromebook_galliumOS"
  echo "22. ezahr commonground"
  echo "23. ezahr devops"
  echo "24. ezahr DigitalOcean"
  echo "25. ezahr huys"
  echo "26. ezahr julia"
  echo "27. ezahr k8s-repo"
  echo "28. ezahr OCI"
  echo "29. ezahr Waardepapieren-AZURE-ACI"
  echo "30. ezahr fail-fast-and-cheap"
  echo "31. ezahr MobileIron template"
  echo "32. ezahr samsungs10e"
  echo "33. ezahr dokuwiki"
  echo "34. ezahr LPC-repo"
  echo "35. ezahr azure-pipelines"
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
         20) git_clone ezahr AZ_ACI_waardepapieren-demo_westeurope_azurecontainer_io ;;
         21) git_clone ezahr chromebook_galliumOS ;;
         22) git_clone ezahr commonground ;;
         23) git_clone ezahr devops ;;
         24) git_clone ezahr DigitalOcean ;;
         25) git_clone ezahr huys ;;
         26) git_clone ezahr julia ;;
         27) git_clone ezahr k8s-repo ;;
         28) git_clone ezahr OCI ;;
         29) git_clone ezahr Waardepapieren-AZURE-ACI ;;
         30) git_clone ezahr fail-fast-and-cheap ;;
         31) git_clone ezahr MobileIron template ;;
         32) git_clone ezahr samsungs10e ;;
         33) git_clone ezahr dokuwiki ;;
         34) git_clone ezahr LPC-repo ;;
         35) git_clone ezahr azure-pipelines  ;;  
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
