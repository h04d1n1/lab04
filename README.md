$ export GITHUB_USERNAME=<имя_пользователя>
$ export GITHUB_EMAIL=<адрес_почтового_ящика>
$ export GITHUB_TOKEN=<сгенирированный_токен>
$ alias edit=<nano|vi|vim|subl>
$ cd ${GITHUB_USERNAME}/workspace
$ source scripts/activate
$ mkdir ~/.config
mkdir: cannot create directory ‘/home/cola/.config’: File exists // Ошибка, потому что у меня папка такая уже существует
$ cat > ~/.config/hub <<EOF
heredoc> github.com:
heredoc> - user: ${GITHUB_USERNAME}
heredoc>   oauth_token: ${GITHUB_TOKEN}
heredoc>   protocol: https
heredoc> EOF
$ git config --global hub.protocol https
$ mkdir projects/lab02 && cd projects/lab02
$ git init
hint: Using 'master' as the name for the initial branch. This default branch name
hint: is subject to change. To configure the initial branch name to use in all
hint: of your new repositories, which will suppress this warning, call:
hint:
hint: 	git config --global init.defaultBranch <name>
hint:
hint: Names commonly chosen instead of 'master' are 'main', 'trunk' and
hint: 'development'. The just-created branch can be renamed via this command:
hint:
hint: 	git branch -m <name>
Initialized empty Git repository in /home/cola/h04d1n1/workspace/projects/lab02/.git/
$ git config --global user.name ${GITHUB_USERNAME}
$ git config --global user.email ${GITHUB_EMAIL}
$ git config -e --global
[credential]
        helper = store
[user]
        email = fedor.z1234@yandex.ru
        name = h04d1n1
[hub]
        protocol = https
$ git remote add origin https://github.com/${GITHUB_USERNAME}/lab02.git
$ git pull origin master

remote: Enumerating objects: 3, done.
remote: Counting objects: 100% (3/3), done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0 (from 0)
Unpacking objects: 100% (3/3), 1.44 KiB | 368.00 KiB/s, done.
From https://github.com/h04d1n1/lab02
 * branch            master     -> FETCH_HEAD
 * [new branch]      master     -> origin/master

$ touch README.md
$ git status
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)
	README.md

nothing added to commit but untracked files present (use "git add" to track)
$ git add README.md
$ git commit -m "Added README.md"
[master 45c4ab3] added README.md
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 README.md
$ git push origin master

 Enumerating objects: 4, done.
Counting objects: 100% (4/4), done.
Delta compression using up to 8 threads
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 278 bytes | 139.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0), pack-reused 0 (from 0)
To https://github.com/h04d1n1/lab02.git
   78306c3..45c4ab3  master -> master
   
$ git pull origin master

remote: Enumerating objects: 4, done.
remote: Counting objects: 100% (4/4), done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0 (from 0)
Unpacking objects: 100% (3/3), 986 bytes | 986.00 KiB/s, done.
From https://github.com/h04d1n1/lab02
 * branch            master     -> FETCH_HEAD
   45c4ab3..726b5af  master     -> origin/master
Updating 45c4ab3..726b5af
Fast-forward
 .gitignore | 4 ++++
 1 file changed, 4 insertions(+)
 create mode 100644 .gitignore
 
$ git log

commit 726b5afd8ab73af0c8d0974e49cbbeb9512c557e (HEAD -> master, origin/master)
Author: h04d1n1 <93523461+h04d1n1@users.noreply.github.com>
Date:   Mon Feb 24 19:17:36 2025 +0300

    Create .gitignore

commit 45c4ab39bac18981287c5540bcc5b132e441122c
Author: h04d1n1 <fedor.z1234@yandex.ru>
Date:   Mon Feb 24 19:13:28 2025 +0300

    added README.md

commit 78306c345ff874ad768cae8d32408703913db20b
Author: h04d1n1 <93523461+h04d1n1@users.noreply.github.com>
Date:   Mon Feb 24 19:08:06 2025 +0300

    Initial commit

$ cat > sources/print.cpp <<EOF
heredoc> #include <print.hpp>
heredoc> void print(const std::string& text, std::ostream& out)
heredoc> {
heredoc>   out << text;
heredoc> }
heredoc> void print(const std::string& text, std::ofstream& out)
heredoc> {
heredoc>   out << text;
heredoc> }
heredoc> EOF

$ cat > include/print.hpp <<EOF
#include <fstream>
#include <iostream>
#include <string>

void print(const std::string& text, std::ofstream& out);
void print(const std::string& text, std::ostream& out = std::cout);
EOF

$ cat > examples/example1.cpp <<EOF
#include <print.hpp>

int main(int argc, char** argv)
{
  print("hello");
}
EOF

$ cat > examples/example2.cpp <<EOF
#include <print.hpp>

#include <fstream>

int main(int argc, char** argv)
{
  std::ofstream file("log.txt");
  print(std::string("hello"), file);
}
EOF

$ edit README.md
$ git status
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)
	examples/
	include/
	sources/

nothing added to commit but untracked files present (use "git add" to track)
$ git add .
$ git commit -m "Added sources"
[master e25ff02] Added sources
 4 files changed, 30 insertions(+)
 create mode 100644 examples/example1.cpp
 create mode 100644 examples/example2.cpp
 create mode 100644 include/print.hpp
 create mode 100644 sources/print.cpp
$ git push origin master
Enumerating objects: 10, done.
Counting objects: 100% (10/10), done.
Delta compression using up to 8 threads
Compressing objects: 100% (7/7), done.
Writing objects: 100% (9/9), 960 bytes | 240.00 KiB/s, done.
Total 9 (delta 0), reused 0 (delta 0), pack-reused 0 (from 0)
To https://github.com/h04d1n1/lab02.git
   726b5af..e25ff02  master -> master
