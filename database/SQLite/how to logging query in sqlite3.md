```c++
static int tracer(unsigned, void*, void*p, void*) 
{
    sqlite3_stmt *stmt = (sqlite3_stmt*)p;

    auto sql = sqlite3_expanded_sql(stmt);

    LOG << sql;

    sqlite3_free(sql);

    return 0;
}

// ~~

sqlite3_open(dbname, &db);
sqlite3_trace_v2(db, SQLITE_TRACE_STMT | SQLITE_TRACE_PROFILE | SQLITE_TRACE_ROW | SQLITE_TRACE_CLOSE, tracer, nullptr);

// ~~
```


### ref  
http://www.sqlite.org/c3ref/profile.html
http://www.sqlite.org/c3ref/trace_v2.html
https://www.sqlite.org/c3ref/c_trace.html
https://stackoverflow.com/questions/1607368/sql-query-logging-for-sqlite
https://stackoverflow.com/questions/39302374/sqlite-log-queries-that-produce-errors
