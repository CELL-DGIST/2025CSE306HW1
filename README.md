## How to use

1. Clone Repository  
  ```
  $ git clone https://github.com/CELL-DGIST/2024CSE306HW1.git
  ```

2. Go to 2024CSE306HW1 Directory.  
  ```
  $ cd 2024CSE306HW1
  ```

3. Run `chmod` to give execute permission.  
  ```
  $ chmod 755 kernelcheck
  ```

4. Execute
  ```
  $ ./kernelcheck
  ```
 - 실행결과로 `encrypted_result.txt` 파일이 생성됩니다.   
   이 파일을 과제로 제출하시면 됩니다.  
 
 - 실행 결과로 터미널에 커스텀 커널을 잘 빌드하였는지 체크결과가 출력됩니다.
    - `Pass!` : 요구사항에 맞게 잘 수행하셨습니다. *encrypted_result.txt*를 제출하세요.
    - `Fail... You need to check again.` : 커널이 잘못 빌드되었습니다. PPT를 보고 Imager 초기화 부터 다시 실행하세요.


<br>
<br>
<br>
<br>

## possible issues

```
1. error while loading shared libraries : libcrypto.so.1.1: cannot open shared object: No such file or directory   
```
제일 마지막 ./kerneltest 단계에서 해당 문제가 발생 가능합니다.   
<br>
원인) 노트북 및 데스크탑에서 필수 패키지들을 설치(apt-get)하는 라이브러리에서 더이상 libcrypto.so.1.1을 지원하지 않음.     
해결 방법)   
    (1) "ldd ./kernelcheck" 확인 시 아래와 같이 shared object file을 찾지 못함. ![오류 상황](./image/error.jpg)
    (2) 아래의 명령어로 libcrypto.so.1.1 파일을 해당 경로로 이동   

    ```
    $ mv ./libcrypto.so.1.1 /lib/aarch64-linux-gnu
    ```
  (3) "ldd ./kernelcheck"로 정상적으로 linking이 되었는지 확인 ![정상](./image/fixed.jpg)

* 주의) 튜토리얼대로 진행했다면, 파일 실행 시 linking을 하기 위해 shared library를 /lib/aarch64-linux-gnu의 경로에서 찾게 됩니다.    
파일 시스템이 다른 구조를 갖는다면 해당 경로가 다를 수 있습니다. 
    
