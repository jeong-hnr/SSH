# bandit 풀이


host: bandit.labs.overthewire.org
port: 2220

0.
username: bandit0, password: bandit0 이므로 접속 명령어 ssh bandit0@bandit.labs.overthewire.org -p 2220를 통해 접속한다. 이후 비밀번호 bandit0를 입력한다.

1.
비밀번호가 home directory의 readme 파일에 있으므로 우선 ls를 한다. readme 파일이 있다고 하므로 cat readme를 통해 내용을 보면 비밀번호는 6y2kwnwK6grgvwvpvLaa2T1cpFEKOhNR 이다.

2.
ls를 하면 파일 이름이 -이므로 cat -는 불가능하고, cat ./-를 통해 현재 폴더에 있는 이름이 '-'인 파일의 내용을 본다. 비번은 PK8fYLZg2hnHSz83plBL1iEPKdD3QToB이다. (./는 현재 디렉토리에 있는 파일이라는 의미)

3.
파일 이름이 --spaces in this filename-- 이므로 -로 시작하는 점과 공백이 있는 점을 해결해야 하므로 cat "./--spaces in this filename--"를 통해 내용을 본다. 비번은 7ZZ2LFrykP2zEyvBl4m3clcL7tGYJPME이다.

4.
ls를 하면 inhere라는 디렉토리가 존재한다고 하므로, cd inhere 후 다시 ls를 한다. 그러나 출력이 없는데, ls -a를 통해 숨겨진 파일 ...Hiding-Form-You를 찾을 수 있다. cat ...Hiding-Form-You를 통해 비번 xzTXq1rDJQVVAzdv5cHq1TQytTWufAMq를 찾는다.

5.
inhere 디렉토리를 확인해보면 -file00 ~ -file09의 파일이 있다. file ./-file 명령어를 통해 파일의 유형을 확인해보면 -file07이 ASCII text라고 하므로 cat ./-file07 명령어를 통해 정답 6C7h9GD8M6ai5nr7wo1RonrzFjj9yIrG를 얻는다.

6.
inhere 디렉토리 안에 maybehere00 ~ maybehere19의 디렉토리가 존재한다. 문제에서 조건을 1033 바이트이고 not executable 이라고 하였으니, find . -type f -size 1033c ! -executable 명령어를 통해 maybehere07 디렉토리의 .file2 파일을 찾아 정답 pXa26xhMWaC2SvDotA4r9EgZkulOeSBW를 얻는다.

7.
서버 어딘가에 파일이 있고, 조건이 owned by user bandit7, owned by group bandit6, 33 bytes in size 이므로 find / -user bandit7 -group bandit6 -size 33c를 하면 Permission denied 메시지가 다수 출력된다. 따라서 2>/dev/null을 붙여 다시 하면 /var/lib/dpkg/info/bandit7.password가 출력되므로 cd /var/lib/dbkg/info 후 cat bandit7.password를 통해 정답 Bmnnvf82KzQlfxgAI2d1zYbr1u9pr3E3를 얻는다.

8.
data.txt를 보면 내용이 너무 많아서 직접 정답을 찾을 수 없으므로, millionth 뒤에 있다는 힌트를 이용하여 grep millionth data.txt를 입력해 정답 VR1ljMayciFxbnUokuQmJFw6QC9VKtub를 얻는다.

9.
정답이 data.txt에서 유일하게 한번 존재하는 내용이라는 힌트가 있으므로, sort data.txt | uniq -u를 통해 정답 EjmOSvuAu7sGAHqHVcBDPirRe9T03kxl를 얻는다.

10.
data.txt의 파일 형식이 binary file이므로 string data.txt | grep =를 통해 읽을 수 있는 부분 중 = 부분을 찾는다. 정답은 B0s2khmbT9u0geKuOoVGW3JZKhndE3BG이다.

11.
base64 인코딩 되어있으므로 base64 -d data.txt를 통해 data.txt를 다시 디코딩하면 정답은 pYfOY6HwUsDj5rL9UvyhU7MCmv8vN5Ro이다.

12.
rot 13이므로 다시 앞으로 13칸 이동하면 된다. cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'을 통해 정답 GROozWPO8QyN0mGrjUkID0WCYkZiQxrN를 얻는다.

13.
파일을 수정해야 하므로 임시 디렉토리를 만들어야 한다. 따라서 mktemp -d를 하고 만들어진 디렉토리로 이동한다. 이제 cp ~/data.txt .를 통해 home 디렉토리의 data.txt를 임시 디렉토리로 복사한다. 우선 16진수 파일이므로 xxd -r data.txt > data를 통해 해제한다. 이제 file data를 하면 gzip 압축되어 있으므로 mv data data.gz, gzip -d data.gz를 통해 압축을 해제한다. file data를 하면 bzip 압축되었으므로 mv data data.bz2, bzip -d data.bz2를 통해 해제한다. 다시 file data를 하면 gzip이므로 위를 반복, 이번에는 POZIX tar archive이므로 mv data data.tar, tar -xf data.tar를 통해 묶음 파일을 해제한다. ls를 하면 data5.bin이 생겼으므로 위 과정을 반복한다. 그럼 data6, data8파일이 나오고 data8파일의 gizp을 해제하면 정답 qQYQiHOBPR8zR61qxYqX45quvihF2uzk이 나온다.

14.
ls를 하면 sshkey.private 파일이 있는데 이것이 개인키이다. 이 개인키를 사용하기 위해 exit 후 mkdir -p ~/.ssh, chmod 700 ~./ssh을 통해 디렉토리를 만든다. 이제 scp -P 2220 bandit13@bandit.labs.overthewire.org:sshkey.private ~/.ssh/bandit14_key를 통해 이 디렉토리에 키 값을 내용으로 하는 bandit14_key라는 파일을 생성한다. 이후 chmod 600 ~/.ssh/bandit14_key를 통해 개인키로 쓰기 위한 권한설정을 하고 ssh -i ~/.ssh/bandit14_key bandit14@banidt.labs.overthewire.org -p 2220을 통해 14에 접속한다. 이제 /etc/bandit_pass/bandit14의 파일내용을 확인해 보면 aaWecNkG4FhxJQxz07uiwzVP6bJiYS65이다.

15.
현재 레벨의 포트 30000에 위 비밀번호를 넣으면 된다고 했으므로 nc localhost 30000 후 비밀번호를 넣으면 정답 pbLYuZtTg4MgaqfJx8jbA9gKKGqM68A7이 나온다.

16.
마찬가지로, 포트 30001에 전송하면 되지만 SSL/TLS 암호화를 사용한다고 하였으므로 openssl s_client -connect localhost:30001 후 위 비밀번호를 전송하면 kS0Hf0u5HiXFwKMKFqXvPdOTNGGa0X8V가 나온다.

17.
localhost의 31000~32000 포트 중 SSL/TLS를 사용하는 하나의 포트에 비밀번호를 보내면 되므로 우선 nmap -p 31000-32000 localhost를 통해 31046, 31518, 31691, 31790, 31960의 open 상태의 포트를 확인했다. 다시 nmap -sV -p 31000-32000 localhost를 통해 31790이 ssl/unknown임을 확인했다. 연결과 비밀번호 전송을 한번에 실행하기 위해 cat /etc/bandit_pass/bandit16 | openssl s_client -connect localhost:31790 -quiet을 실행하면 개인키가 나온다. 개인키 전체를 복사한 후 개인키 파일을 만들기 위해 nano /tmp/bandit17_key 후 개인키를 붙여넣고 chmod 600 /tmp/bandit17_key로 권한을 설정하고 ssh -i /tmp/bandit17_key bandit17@bandit.labs.overthewire.org -p 2220으로 접속한다.

18.
두 파일 중 passwords.new에만 있는 내용이 정답이므로 diff passwords.new passwords.old를 통해 < 부분의 OQxXZjELndr90zuhOTDYBEomI0SZITXI를 알아내었다.

19.
18의 비밀번호는 알아냈지만 접속하여 SSH에 로그인되어 쉘이 켜지는 순간 수정된 .bashrc가 실행돼 로그아웃된다. 따라서 쉘을 켜지 않고 SSH로 명령어 하나만을 실행해야 한다. 이를 통해 정답 KpsOfPkcP7i1FlIExk2QEjyt6dw8dxZI를 알아내었다.

20.
ls-l을 실행하면 bandit20-do라는 파일이 -rws...로, setuid 실행파일임을 알 수 있다. ./bandit20-do를 하면 뒤에 명령어를 붙여서 사용할 수 있다고 한다. 정답은 일반적인 위치인 /etc/bandit_pass에 있으며 실행파일 실행 후 내용을 볼 수 있다고 한다. 따라서 ./bandit20-do cat /etc/bandit_pass/bandit20을 통해 정답 4pIjcunZ0fK2vmp3IwfG8Vf7VhxD6pOA를 얻어냈다.

21.
ls -l을 하니 -rws...의 setuid 실행파일 suconnect가 있음을 확인했다. ./suconnet를 하니 뒤에 포트번호를 붙여 실행하면 상대편에서 비밀번호를 받으면 다음 비밀번호를 답신한다는 설명이 나온다. 따라서 다른 터미널을 열어 다시 bandit20에 접속하고 nc -l -p 12345를 통해 임시 포트를 열고 기다린다. 원래 포트에서 ./suconnect 12345를 실행하고 반대편 터미널에서 bandit20의 비밀번호를 입력하면 해당 터미널에 답변으로 bandit21의 비밀번호 bW9kBv5WC3P4yoDyf12LSdGuNz5ka6hY이 전송된다.

22.
안내대로 /etc/cron.d/에 가서 ls -l을 해보면 cronjob_bandit22라는 파일이 있으므로 cat cronjob_banit22를 해본다. 그러면 "* * * * * bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null" 라는 내용이 있는데 이는 매분마다 bandit22의 권한으로 /usr/bin/cronjob_bandit22.sh를 실행한다는 뜻이다. 따라서 다시 cat /usr/bin/cronjob_bandit22.sh를 하면 "cat /etc/bandit_pass/bandit22 > /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv" 라는 내용이 있는데, 이는 /etc/bandit_pass/bandit22의 내용을 /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv에 복사한다는 내용이므로 마지막으로 cat /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv를 하면 정답 RYVux2rHEm9tiXHmLFzuR7Vhx6AZQMEz가 나온다.

23.
etc/cron.d/의 cronjob_bandit23 내용을 보면 "* * * * * bandit23 /usr/bin/cronjob_bandit23.sh  &> /dev/null" 가 있고 이는 /usr/bin/cronjob_bandit23.sh를 매분 실행한다는 뜻이므로 다시 /usr/bin/cronjob_bandit23.sh를 cat하면

#!/bin/bash

myname=$(whoami)
mytarget=$(echo I am user $myname | md5sum | cut -d ' ' -f 1)

echo "Copying passwordfile /etc/bandit_pass/$myname to /tmp/$mytarget"

cat /etc/bandit_pass/$myname > /tmp/$mytarget

이라는 내용이 나온다. myname은 bandit23으로 작동하며 따라서 echo I am user bandit23 | md5sum | cut -d ' ' -f 1 을 실행해보면 8ca319486bfbbc3663ea0fbe81326349 이라는 해시값이 나오고, 이 해시값이 주로소 들어가는 /tmp/8ca319486bfbbc3663ea0fbe81326349에 정답 gKXDTAXnIz3OBxiPjRZ2uqutUlPZrBsw 가 저장되어 있다.

24.
우선 cat /etc/cron.d/cronjob_bandit24를 하면

* * * * * bandit24 /usr/bin/cronjob_bandit24.sh &> /dev/null

과 같은 내용이 있는데, 따라서 다시 cat /usr/bin/cronjob_bandit24.sh를 하면

#!/bin/bash

shopt -s nullglob

myname=$(whoami)

cd /var/spool/"$myname"/foo || exit
echo "Executing and deleting all scripts in /var/spool/$myname/foo:"
for i in * .*;
do
    if [ "$i" != "." ] && [ "$i" != ".." ];
    then
        echo "Handling $i"
        owner="$(stat --format "%U" ./$i)"
        if [ "${owner}" = "bandit23" ] && [ -f "$i" ]; then
            timeout -s 9 60 "./$i"
        fi
        rm -rf "./$i"
    fi
done

의 구조가 나온다. 이 스크립트의 역할을 정리해보면 /var/spool/bandit24/foo 내부의 모든 파일들을 순회하면서 소유자가 bandit23이고 일반 파일이라면 bandit24의 권한으로 실행하고 해당 파일을 삭제하는 것이다. 따라서 힌트를 따라 공용 /tmp에 랜덤 디렉토리를 만들어본다.

WORKDIR=$(mktemp -d /tmp/bandit23.XXXXXX)를 입력하고 echo "$WORKDIR"로 확인해보면

/tmp/bandit23.aXfipl

가 출력되었다. 이제 bandit23에는 읽기, 쓰기, 실행 권한을 모두 부여하고 bandit24에는 쓰기와 실행 권한을 부여하기 위해 chmod 733 "$WORKDIR"를 실행한다. 이렇게 하면 bandit24가 이 디렉토리 내부에 파일을 만들 수 있다. 이후

cat > "$WORKDIR/getpass.sh" <<EOF
#!/bin/bash
cat /etc/bandit_pass/bandit24 > "$WORKDIR/password"
chmod 644 "$WORKDIR/password"
EOF

로 스크립트를 만들고 저장해주었다. 그 후 chmod 755 "$WORKDIR/getpass.sh"로 소유자가 아닌 사용자 bandit24에도 스크립트의 실행 권한을 부여한다.

이제 JOBNAME="job_$(basename "$WORKDIR").sh" 로 임시 디렉토리 이름을 만들고
cp "WORKDIR/getpass.sh" "/var/spool/bandit24/foo/$JOBNAME" 으로 스크립트를 cron의 대상이 되는 폴더에 복사한다.

cron이 실행될 때까지 기다렸다가 ls -l "$WORKDIR" 로 확인해주면 password라는 파일이 생성되었음을 확인할 수 있고, cat "$WORKDIR/password"를 통해 비밀번호 hVQMk3lJNsmQ7VF3ubyrNNBom7BOgVXv를 얻었다.

25.
