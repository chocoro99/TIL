# 매일 사용한 순서로 작성

# poetry 설치

## 윈도우(파워쉘)

    (Invoke-WebRequest -Uri https://install.python-poetry.org -UseBasicParsing).Content | py -


C:\Users\(사용자이름)\AppData\Roaming\Python\Scripts - 환경변수 path 설정

## vscode에서

    poetry  
    poetry init enter enter enter enter 라이선스:MIT enter no no yes  
    poetry add django

## vscode 오류 시  
윈도우 powershell 관리자 실행  

    get-ExecutionPolicy - 현재 권한 확인  
    Set-ExecutionPolicy RemoteSigned - 권한을 RemoteSigned로 변경 질문엔 Y  
    get-ExecutionPolicy - 권한이 변경 됐는지 확인  
vscode 재 실행 후 오류 발생 여부 확인

### poetry 접속 : poetry shell  
### poetry 종료 : exit

poetry 접속 후 django-admin startproject config .  
vscod 확장 프로그램 gitignore extension 설치  
View - Command Pallatte - add gitignore - python

### 서버 실행 : python manage.py runserver
### 서버 종료 : ctrl + c

# 애플리케이션 구축

    python manage.py startapp 이름  
    python manage.py migrate 실행

# 관리자 계정 만들기

    python manage.py createsuperuser (enter)  
    id 입력  
    password 입력

# DateTimeField

    class DateTimeField(auto_now=False, auto_now_add=False, \*\*options)

Python에서 datetime.datetime 인스턴스로 표시되는 날짜 및 시간입니다.  
DateField와 동일한 추가 인수를 사용합니다.

auto_now : 개체를 저장할 때마다 자동으로 현재 시간으로 설정합니다.  
마지막으로 수정한 타임스탬프에 유용합니다.

auto_now_add : 개체를 처음 만들 때 자동으로 현재 시간으로 설정합니다.

# CharField

    class CharField(max_length=None, \*\*options)

작은 문자열에서 큰 문자열에 대한 문자열 필드입니다.  
많은 양의 텍스트의 경우 텍스트 필드를 사용합니다.

max_length : 최대 글자 수를 정합니다 ex) max_length=140

# TextField

    class TextField(\*\*options)

큰 텍스트 필드입니다.

# ImageField

    class ImageField(upload_to=None, height_field=None, width_field=None, max_length=100, \*\*options)

height_field : 이미지의 높이를 자동으로 채워주는 모델 필드입니다.  
width_field : 이미지의 너비를 자동으로 채워지는 모델 필드의 이름입니다

## ImgeField 사용
    settings.py  
    import os  
    MEDIA_URL = '/media/'  
    MEDIA_ROOT = os.path.join(BASE_DIR, 'media')
ImageField(upload_to="media")  

## error 발생 시
pillow 설치합니다   
또는  
python manage.py makemigrations  
python manage.py migrate를 안해서 생기는 오류

# django admin
    from django.contrib import admin  
    from .models import test -> 만들어 둔 모델 불러오기

    @admin.register(test) -> decorator 모델 통제 역할   
    class testAdmin(admin.ModelAdmin): -> admin.ModelAdmin을 상속  
    pass

    python manage.py makemigrations : 장고에서 마이그레이션 자동 생성 명령어  
    python manage.py migrate : 마이그레이션을 통해 데이터베이스 모양으로 업데이트 한 것을 데이터베이스에게 요청  
http://localhost:8000/admin 에서 확인

# __ str __ 메소드
__str __ 는 해당 클래스로 만들어진 인스턴트를 자체를 출력할 때,  
문자열로 설명해주기 위한 메소드다.   

    model.py  
    class Test(models.Model):  
    test_text = models.CharField(max_length=140)  
    def __str__(self):  
    return self.test_text

# list_display, list_filter, search_fields
django admin에서 보여주는 컬럼과 필터, 그리고 검색 기능

    model.py  
    class Test(models.Model):  
    test_text = models.CharField(max_length=140)  
    test_title = models.CharField(max_length=140)  
    test_date = models.DateTimeField(auto_now = True)

    admin.py  
    from .models import Test
    @admin.register(Test)  
    class TestAdmin(admin.ModelAdmin)  
    list_display = ("test_title","test_date") -> 화면에 보여지는 리스트  
    list_filter = ("test_date) -> 날짜로 필터  
    search_fields = ("test_title") -> 제목으로 검색

# migration 삭제
각각의 폴더 안에 migrations 안에 _initial.py 파일 삭제  
python manage.py makemigrations

# AUTH_USER_MODEL
AUTH_USER_MODEL = "사용할 users"


# 장고 first_name, last_name 막기
    models.py에서  
    first_name = models.CharField(max_length=150, editable=False)  
    last_name = models.CharField(max_length=150, editable=False)  
    editable=False로 사용하지 않게 막기

# fieldsets
수정 페이지 내용을 커스텀

    admin.py   
    fieldsets = ((None, {"fields": ("username")))

# DRF(Django REST Framework) 설치 및 사용
Django 기반 REST API 서버를 만들기 위한 라이브러리 설치 

    poetry add djangorestframework

config/settings.py 파일에 DRF(Django REST Framework) 등록하기 

    INSTALLED_APPS = ['rest_framework']

# 회원가입
    config/settings.py  
    INSTALLED_APPS = ['rest_framework.authtoken'] : 기본 토큰 인증 방식  
    REST_FRAMEWORK = {'DEFAULT_AUTHENTICATION_CLASSES':   
    ['rest_framework.authentication.TokenAuthentication']  
    }

users 폴더에 serializers.py 파일 생성  
serializer : Django 프로젝트에서 모델 인스턴스를 JSON 타입으로 바꾸는 것  

    users/serializers.py  
    from .models import 클래스  
    from django.contrib.auth.password_validation import validate_password : Django의 기본 패스워드 검증 도구  
    from rest_framework import serializers
    from rest_framework.authtoken.models import Toke : Token 모델  
    from rest_framework.validators import UniqueValidator : 이메일 중복 방지 검증 도구  

    class RegisterSerializer(serializers.ModelSerializer):  
    email = serializers.EmailField(  
        required=True, validator=  
        [UniqueValidator(   
            queryset=User.objects.all()  
            )]) : 이메일 중복 검증  
    password = serializers.CharField(  
        write_only=True,  
        required = True,  
        validdator=[validdate_password]  
        class Meta:  
        model = User  
        fields = ("email","password")  
        def create(self, validate_data):  
        user = User.objects.create_user(  
            email = validate_data["email"],  
            password = validate_data["password"]  
            user.save()  
            token = Token.objects.create(user=user)  
            return user  
        )
    )  

View : 템플릿과 모델 사이를 이어주는 다리 역할  

    users/views.py
    from .models import User  
    from rest_framework import generics  
    from .serializers import RegisterSerializer  

    CreateAPIView(generics) 사용 구현  
    class RegisterView(generics.CreateAPIView):  
    queryset = User.objects.all()  
    serializer_class = RegisterSerializer  

URL(Uniform Resource Locator) : 라우팅의 역할과 서버로 해당 주소에 할당된 리소스를 요청하는 역할  

    users/urls.py  
    from django.urls import path  
    from .views import RegisterView  
    urlpatterns =  [    
        path('register', RegisterView.as_view())  
    ]  

    confgi/urls.py
    from django.urls import path, include  
    from django.contirb import admin  
    urlpatterns = [  
        path('admin/', admin.site.urls),  
        path('users/', include('users.urls'))  
    ]  
다 적용 후  
python manage.py makemigrations - migrate - runserver로 실행 및 확인

https://insomnia.rest/download로 확인 가능

# Django 로그인 serializer, Token

    users/serializers.py
    from django.contrib.auth import authenticate # Django의 기본 authenticate 함수, TokenAuth 방식으로 유저를 인증

    class LoginSerializer(serializers.Serializer):
        email = serializers.CharField(required=True)
        password = serializers.CharField(required = True, write_only=True) # write_only는 클라이언트 -> 서버 방향으로의 역직렬화만 가능
        
        def validate(self, data):
        user = authenticate(**data)
        if user:
        token = Token.objects.get(user=user)
        return token
        raise serializers.ValidationError(
            {"error": "Unable to log in with provided credentials."}
        )

users/views.py GenericAPIView를 사용한 구현, POST 요청으로 1차적인 보안과 토큰을  그대로 응답하는 방식의 구현   

    from rest_framework import generics, status
    from rest_framework.response import Response
    from .serializers import RegisterSerializer, LoginSerializer

    class LoginView(generics.GenericAPIView):
    serializer_class = LoginSerializer

    def post(self, request):
    serializer = self.get_serializer(data=request.data)
    serializer.is_valid(raise_exception=True)
    token = serializer.validated_data
    return Response({"token":token.key}, status=status.HTTP_200_OK)
