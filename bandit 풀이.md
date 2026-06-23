# bandit 풀이


host: bandit.labs.overthewire.org
port: 2220
username: bandit0
password: bandit0 이므로 접속 명령어 ssh bandit0@bandit.labs.overthewire.org -p 2220를 통해 접속한다. 이후 비밀번호 bandit0를 입력한다.
1.
비밀번호가 home directory의 readme 파일에 있으므로 우선 ls를 한다. readme 파일이 있다고 하므로 cat readme를 통해 내용을 보면 비밀번호는 ZjLjTmM6FvvyRnrb2rfNWOZOTa6ip5lf 이다.
2.
ls를 하면 파일 이름이 -이므로 cat -는 불가능하고, cat ./-를 통해 현재 폴더에 있는 이름이 '-'인 파일의 내용을 본다. 비번은 263JGJPfgU6LtdEvgfWU1XP5yac29mFx이다.
3.
파일 이름이 --spaces in this filename-- 이므로 -로 시작하는 점과 공백이 있는 점을 해결해야 하므로 cat "./--spaces in this filename--"를 통해 내용을 본다. 비번은 MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx이다.
4.