# SQLite 데이터베이스 락 방지하기
---
## SQLite Lock 왜 발생할까?

## How to avoid SQLite lock?
### 타임아웃처리
- sqlite3_busy_timeout()
### 인스턴스(sqlite3*) 싱글턴
### 트랜잭션 순차처리 강제

### 참조
https://sqlite.org/lockingv3.html
https://www.sqlite.org/faq.html
https://programmingfbf7290.tistory.com/entry/SQLite-주의할-점-및-팁DB-락
https://stackoverflow.com/questions/17348480/how-do-i-prevent-sqlite-database-locks  
https://stackoverflow.com/questions/30438595/sqlite3-ignores-sqlite3-busy-timeout
https://stackoverflow.com/questions/4101837/avoiding-sqlite3-database-locked
https://stackoverflow.com/questions/24598721/how-can-i-check-if-sqlite-database-is-open-in-c-c
