source "https://rubygems.org"
gemspec
gem "webrick", "~> 1.7"

# Windows does not include zoneinfo files, so bundle the tzinfo-data gem
# 검색해서 찾아보니 windows에는 루비 인터프리터가 IANA 타임존 정보를 처리하는데 필요한 정보 원천이 없어서, 환경변수인 TZ를 사용한다고 한다. 아래 문구를 추가해서 local 연결(http://127.0.0.1:4000/)에러 해결
gem 'tzinfo'
gem "tzinfo-data", platforms: [:mingw, :mswin, :x64_mingw, :jruby]
