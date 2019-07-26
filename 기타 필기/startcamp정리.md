## StartCamp Day 1

#### 1.  auto_browser.py ( 파이썬에서 브라우저 열기)

```python
import webbrowser #웹브라우저 열기위한 모듈

idols = ['iu', 'bts', 'ziont']

for idol in idols: #idols라는 리스트 안에 idol이라는 변수 생성
   webbrowser.open(f'https://google.com/search?q={idol}') #f:문자열포멧팅
```

**라이브러리 설치**

```git bash
$ pip install requests
$ pip install os
```



#### 2. requests.py (필요한 페이지 가지고 오기)

```python
import requests # 파이썬에서 요청하는 모듈
import bs4 # BeautifulSoup: 받은 문서를 보기좋게, 검색하기 좋게 만들어줌

url = 'https://finance.naver.com/sise/' # 내가 따올 내용이 있는 페이지 url

response = requests.get(url) 
              # 페이지에 get요청을 보냄(내가 가지고갈테니 따올 내용을 보여달라)
print(response.status_code) # 200:존재하는 페이지, 404:존재하지 않는 페이지

html = response.text # 페이지 파일 전체를 텍스트 파일로 가짐
			     # 전부 다 문자열(str)->우리가 원하는 정보만 얻게하는 것(bs4)

soup = bs4.BeautifulSoup(html, 'html.parser')
# parser:text로 되어있어 우리가 접근 못하는 것들을 접근가능한 형태로 바꿔주는 것

kospi = soup.select_one('#KOSPI_now').text # 요소검사에서 페이지에서 필요한 것 누르면 이름 알려줌(ex.KOSPI_now -> 이는 selector 경로)
# soup.select_one(selector): 문서 안에 있는 특정 내용을 하나만 뽑음(변수)
# soup.select(selector): 문서 안에 있는 특정 내용을 모두 뽑음(리스트 형태)

print(kospi)
```



## StartCamp Day 2

#### 1.  naver_rank.py ( 네이버 실시간검색어 추출)

```python
import requests
import bs4

url = 'https://www.naver.com/'

selector = '.ah_k' #class selector이다 (이렇게 생긴 것을 추출하겠다)

html = requests.get(url).text
soup = bs4.BeautifulSoup(html, 'html.parser')
ranks = soup.select(selector)
print(rank) # <span class="ah_k">티르티르</span> 이렇게 출력됨

for rank in ranks: # for문을 쓰는 이유: 실검(한글)단어만 뽑고 싶다.
    print(rank.text) # 티르티르
    				 # 정글의법칙..
```



#### 2. txt_read.py txt_write.py ( csv 이용한 읽기, 쓰기 )

###### txt.read.py

```python
# 1번
f = open('ssafy_txt', 'r')
all_text = f.read() # text전체를 불러옴(개행문자 포함!)
print(all_text)
f.close()

# 2번
with open('with_ssafy.txt', 'r') as f:
    all_text = f.read()
    print(all_text)

# 3번
with open('with_ssafy.txt', 'r') as f:
    lines = f.readlines() # 파일 전체를 읽은 다음 라인을 리스트로 읽어옴
    					  # lines에 this is line1~10까지 있다
    for line in lines:
        print(line.strip) #.strip():개행문자 제거

# 4번(csv)
import csv
with open('dinner.csv', 'r', encoding='utf-8') as f: 
    								#utf-8: 한글, 중국어, 이모티콘 해석위함
    items = csv.reader(f)
    for item in items:
        print(item)

```

###### txt.write.py

```python
# 1번
f = open('ssafy_txt', 'w')
for i in range(10):
    f.write(f'this is line {i+1}\n') #\n: 그다음 줄로 내리겠다
f.close()#.close()해줘야 내용 날라가는 것을 방지할 수 있음

# 2번
with open('withssafy_txt', 'w') as f:
    for i in range(10):
        f.write(f'this is line {i+1}\n')

# 3번
with open('withssafy_txt', 'w', encoding='utf-8') as f:
    f.writeline(['0\n', '1\n', '2\n', '3\n'])
    
# 4번(csv)
import csv
with open('dinner.csv', 'w', encoding='utf-8', newline='') as f:
    #newline='' -> 두줄씩 띄지 않음
    csv_writer = csv.writer(f)
    for item in dinner.items():
        csv_writer.writerow(item)
        
```



#### 3. ssafy_txt파일을 읽어서 역순으로 reversed_ssafy.txt 파일로 저장

```python
with open('ssafy_txt', 'r') as f:
    lines = f.readlines()
    
lines.reverse() #해당리스트 뒤집기    

with open('reversed_ssafy_txt', 'w') as f:
    for line in lines:
        f.write(line)
```



#### 4. 랜덤으로 500명 이름 만들기

```python
import os
import random

f = ['김','이','박','최','황','오','강','한','제갈','하','정','송', '현']
g = ['길동', '준', '민준','소미','수진','지은','동해','민태','준호', '세정']

for i in range(500):
    cmd = f'touch {i + 1}_{random.choice(f)}{random.choice(g)}.txt'
    print(cmd)
    os.system(cmd) #시스템 명령어 호출하기

```



## StartCamp Day 3

#### 1.  bithumb에 있는 코인 정보 가지고오기

```python
# 1. Bithumb 페이지를 가지고 온다.
import requests
import bs4
import csv

response = requests.get('https://www.bithumb.com/') 
	# 요청을 보내 응답을 받음 # url의 전체 가지고옴

html = response.text
	# 응답받은 객체에서 html 문서를 string으로 가지고 옴
    # 현재 html의 타입은? string(문자) -> 이는 html형태가 아니라 그냥 문자 
    # ->의미없음-> class, id, tag로 접근가능하게 beuatifulsoup 사용

    
# 2. BeautifulSoup 모듈을 이용하여 string type의 html을 파싱한다.
soup = bs4.BeautifulSoup(html, 'html.parser') 
	#우리가 가지고온 html문서를 파싱한 결과->우리가 가지고 올 수 있는 객체가 됨

    
# 3.각 코인의 정보가 담겨있는 table row 데이터를 list의 형태로 가져오기
    # 한 줄을 item으로 삼고 모든 tr을 하나의 리스트로 가지고 옴(btc, eth,..)
coins = soup.select('.coin_list tr') 
	#coin_list 안에 있는 tr에 접근하겠다. 
    # 필요한 것들을 선택 #coins는 <tbody coin_list>밑에 있는 tr들 가지고옴
    # .coin_list tr: class가 가지고 있는 모든 하위tr 가지고옴
    # .coin_list > tr: 무조건 coin_list 바로 밑에 있는 tr을 가지고 와라

    
# 4. 각 코인을 순회하며 필요한 정보만 추출한다.
for coin in coins: # coin == tr
   coin_name = coin.select_one('td:nth-child(1) > p > a> strong').text 
    	# 단어만 빼내겠다.
    coin_name = coin_name.replace("NEW", '')
    	# coin_name = coin.select_one('td:nth-child(1) > p > a> 
    	# strong').text.replace("NEW", '') 해도 같은 결과
        # .replace()는 문자열 자료형에 사용
    coin_price = coin.select_one('td:nth-child(2) > strong').text
    print(coin_name, coin_price)
    	# coin: 각각 하나의 tr, coins: tr 전체
    	# 각 코인의 이름과 시세, 데이터를 추정
    	# coin_name 때 활용 tableAsset > tbody > tr:nth-child(1) 
        # [여기까지 coin] > td:nth-child(1)
    	# coin_price 때 활용 tableAsset > tbody > tr:nth-child(1) > 
        # td:nth-child(2)

        
# 5. csv writer를 이용해 정보를 저장한다.
with open('coin_info.csv', 'w', encoding='utf-8', newline='') as f:
    csv_writer = csv.writer(f) # csv_writer한테 파일 전체 넘겨주기

    
#6. 보낼 정보를 만든다
    for coin in coins: # coin == tr
        coin_name = coin.select_one('td:nth-child(1) > p > a> strong').text.replace("NEW", '').strip()
        coin_price = coin.select_one('td:nth-child(2) > strong').text 
            # 가격이 천원 이상이면 ,가 생김 -> 따라서 ""로 감싸서 하나의 데이터
            # 로 만든다는 것 -> 1000원 미만의 것은 ""생기지 않음  # 원, 
            # ','지우면 조금 더 깔끔하게 나옴
            # :nth-child가 있어야 (3)이나 (2)를 쓸 수 있다!
        data = (coin_name, coin_price) # 튜플형식으로 만들어주기!!! 
        csv_writer.writerow(data) # strip():공백지우기
        print(data)

```



#### 2. html (문서로서 정보 제공 = 정보의 구조화)

```html
<!DOCTYPE html>
<html lang="en">
<head> <!--head : 문서의 정보를 가지고 있다.-->
    <title>네이버</title>
    <link rel="stylesheet" href="style.css"> 
    				<!--href="styple.css"는 style.css파일에서 꾸며주겠다는 의미-->
</head>
<body> <!--body : 실제로 브라우저에서 보이는 내용-->
    <h1>SSAFY_2기</h1>
    <h2>HTML + CSS 맛보기</h2>
    <h2 style="color:forestgreen">즐거운 코딩</h2>
    <p id="description">문단 구분 p 태그</p> <!--id는 하나만 있어야함-->
    <span>문단을 구분하지 않습니다.</span> <!--문단 구분하지 않음-->
    <span>하하</span>
    <ol> <!--리스트를 작성 가능-->
        <li class="list-item">이건 순서가 있는 태그</li> <!--li: 항상 ol 안에 존재-->
        <li class="list-item">이건 순서가 있는 태그</li> <!--class는 유일할 필요X-->
        <li class="list-item">이건 순서가 있는 태그</li> 
    </ol>
    <ul>
        <li>이건 순서가 없는 태그</li>
        <li>이건 순서가 없는 태그</li>
        <li>이건 순서가 없는 태그</li>
    </ul>
</body>
</html>
```



#### 3. css (스타일링의 정의)

```css
/* 요소 선택자(type) */
h2 {
    color:darkolivegreen;
}

/* 아이디 선택자(id) - 아이디는 유일 */
#description {
    background-color:lightblue; 
}

/* 클래스 선택자(class)(li.list-item가능, .list-item가능) */
li.list-item {
    font-size: 20px;
}

/* ul 안에 있는 li 선택 */
ul li {
    background-color: cornflowerblue;
}
```



## StartCamp Day 4

#### 1.  flask

- 필요한 flask

  ​		1.사용자가 input(정보)을 입력할수있는 페이지 

  ​		2.사용자가 페이지를 통해 우리에게 제출하면 계산 후 사용자에게 다시 보내주는 페이지

- ex. 나이 입력하면 나이와 다른 말 뽑아냄

  ```python
  @app.route('/ping')
  def ping():
      return render_template('ping.html') # 요청 : /pong?age=24 / html만듦
  #html
  # form actio="/주소창의?전까지"
  # input type="text/number" name="변수이름(?뒷 단어)"
  # button type="submit"
  
  
  @app.route('/pong')
  def pong():
      age = request.args.get('age') # 사용자가 보낸 입력값에서 꺼내겠다
      return f'Pong! age: {age}'
  ```

- 사용자가 보낸 input값을 request함수를 통해 받는다.
-  요청보내는 것 = requests함수를 통해 url에 붙여 보낸다.



# day4(startcamp)

만약 우리한테 작성할 수 있게 설문지 form을 주심. 이름, 이메일, github아이디를 작성하고 다시 선생님께 드려야함. -> 우리의 정보를 알고 slack이나 github에서 초대하는 듯한 행동을 할 수 있음<실습-ping_pong>

ex1. 로그인( 사용자 input 받음 )

1. 로그인 페이지가 먼저 필요하고 거기에서 아이디와 비번을 적을 수 있어야한다
2. 로그인을 했다면, 그 정보가 넘어온다. -> 그러면 확인하고 로그인 시키는 방법

- 이런 작업들을 하려면 사용자가 하는 것은 우리에게 요청을 보내는 것. 우리는 요청을 받을 수 있는 경로가 있어야함.(ex.요청 -> 로그인 페이지 주세요 )
- 로그인 할께요라고 요청하는 페이지 하나, ID와 비번을 입력한 후 인증 요청 페이지 하나

ex2. 검색 ( 사용자 input 받음 )

검색도 마찬가지. -> 사용자 정보 받고 이런 키워드에 관심있다는 것을 인지.

- 검색 해주세요라는 요청 하나, 검색 결과 알려달라는 요청 하나

## 실습

/pong?age=안녕하세요(주소창)



## API 사용방법 무조건 알고있어야함!

- 내가 가진 형태(규칙대로)로 정보를 입력해 나한테 요청하면 내가 줄 수 있다.

- http://artii.herokuapp.com/make?text=HelloWorld 

  :  text값에 넣어야 값을 우리에게 제공해줌 -> text값을 넘겨주는 것이 필요

  ​		 :  ~ make까지 form에 넣고, input name에 HelloWorld 입력(띄어쓰기도 가능!)

- 랜덤으로 fonts 뽑아서 사용자에게 보여주는 서비스 but 복잡

- 이 작업이 필요! 

  local host어디선가 flask가 있음. 이때 ascii art로 사용자가 어떤 특정 문자열을 입력해서 보내면(HelloWorld) string형태로 가지고있음. 이 형태를 ascii art라는 API에게 먼저 어떤 폰트를 가지고 있는지 물어보고(flask가 API한테 요청함) 그 중 하나만 뽑아서 HelloWorld랑 조합해서 API한테 만들어달라고 요청하면 그쪽에서 우리한테 만들어줌 그것을 사용자에게 제공해줌

  input 





##### API = Application Program Interface

내가 원하는 서비스를 제공하고 싶을 때, 다른 프로그램에서 나한테 접근해서 제공을 받고싶을 때 지켜야하는 약속들(ex. 우편보낼 때 받는 사람,주소,번호, 보내는 사람,주소,번호 작성해야함)

##### HTML              ///     Flask

정적인 웹           동적인 웹

##### request & response

request : 네이버로 요청 보내는 것

response : 네이버가 응답해줌 -> 응답받은 우리는 잘 읽어 이쁘게 화면에 보여줌 (응답받을수있는것 있음 - json, text, html )

##### JavaScript 

동적으로 작동



#### jupyter 사용법

jupyter notebook은 켜둬야한다.   Ctrl + c -> 꺼짐

git bash는 리눅스 기반의 tab이므로 

vi ~/.bashrc : i 누르고 내용작성

cat. bashrc -> 안에 내용물 알려줌

touch .bash_profile -> touch는 새로운 빈 파일을 설정

