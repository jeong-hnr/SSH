# bandit 풀이


host: bandit.labs.overthewire.org
port: 2220
username: bandit0
password: bandit0 이므로 접속 명령어 ssh bandit0@bandit.labs.overthewire.org -p 2220를 통해 접속한다. 이후 비밀번호 bandit0를 입력한다.
1.
비밀번호가 home directory의 readme 파일에 있으므로 우선 ls를 한다. readme 파일이 있다고 하므로 cat readme를 통해 내용을 보면 비밀번호는 ZjLjTmM6FvvyRnrb2rfNWOZOTa6ip5lf 이다.
2.
ls를 하면 파일 이름이 -이므로 cat -는 불가능하고, cat ./-를 통해 현재 폴더에 있는 이름이 '-'인 파일의 내용을 본다. 비번은 263JGJPfgU6LtdEvgfWU1XP5yac29mFx이다. (./는 현재 디렉토리에 있는 파일이라는 의미)
3.
파일 이름이 --spaces in this filename-- 이므로 -로 시작하는 점과 공백이 있는 점을 해결해야 하므로 cat "./--spaces in this filename--"를 통해 내용을 본다. 비번은 MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx이다.
4.
ls를 하면 inhere라는 디렉토리가 존재한다고 하므로, cd inhere 후 다시 ls를 한다. 그러나 출력이 없는데, ls -a를 통해 숨겨진 파일 ...Hiding-Form-You를 찾을 수 있다. cat ...Hiding-Form-You를 통해 비번 2WmrDFRmJIq3IPxneAaMGhap0pFhF3NJ를 찾는다.
5.
inhere 디렉토리를 확인해보면 -file00 ~ -file09의 파일이 있다. file ./-file 명령어를 통해 파일의 유형을 확인해보면 -file07이 ASCII text라고 하므로 cat ./-file07 명령어를 통해 정답 4oQYVPkxZOOEOO5pTW81FB8j8lxXGUQw를 얻는다.
6.
inhere 디렉토리 안에 maybehere00 ~ maybehere19의 디렉토리가 존재한다. 문제에서 조건을 1033 바이트이고 not executable 이라고 하였으니, find . -type f -size 1033c ! -executable 명령어를 통해 maybehere07 디렉토리의 .file2 파일을 찾아 정답 HWasnPhtq9AVKe0dmk45nxy20cvUa6EG를 얻는다.
7.
서버 어딘가에 파일이 있고, 조건이 owned by user bandit7, owned by group bandit6, 33 bytes in size 이므로 find / -user bandit7 -group bandit6 -size 33c를 하면 Permission denied 메시지가 다수 출력된다. 따라서 2>/dev/null을 붙여 다시 하면 /var/lib/dpkg/info/bandit7.password가 출력되므로 cd /var/lib/dbkg/info 후 cat bandit7.password를 통해 정답 morbNTDkSW6jIlUc0ymOdMaLnOlFVAaj를 얻는다.
8.
data.txt를 보면 내용이 너무 많아서 직접 정답을 찾을 수 없으므로, millionth 뒤에 있다는 힌트를 이용하여 grep millionth data.txt를 입력해 정답 dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc를 얻는다.
9.
정답이 data.txt에서 유일하게 한번 존재하는 내용이라는 힌트가 있으므로, sort data.txt | uniq -u를 통해 정답 4CKMh1JI91bUIZZPXDqGanal4xvAg0JM를 얻는다.