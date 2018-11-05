# node-api-postgres
Node Express Posgresql

[Setting up a RESTful API with Node.js and PostgreSQL](https://blog.logrocket.com/setting-up-a-restful-api-with-node-js-and-postgresql-d96d6fc892d8?fbclid=IwAR1fbBLEsK3jgIgQ26vlUBmBJrk81C6C1C5_zij2v-JpEIJoScoL5biP5kU)

을 따라하면서 막히는 부분 수정

* PostgreSQL 설치 및 실행
* createUser result 오타 및 returning ID 부분 처리



## 1. PostgreSQL 인스톨 및 실행

<pre>

brew install postgresql

brew services stop postgresql

pg_ctl -D /usr/local/var/postgres start
  <code>
    waiting for server to start....2018-11-05 15:02:53.444 KST [41568] LOG:  listening on IPv6 address "::1", port 5432
    2018-11-05 15:02:53.444 KST [41568] LOG:  listening on IPv4 address "127.0.0.1", port 5432
    2018-11-05 15:02:53.445 KST [41568] LOG:  listening on Unix socket "/tmp/.s.PGSQL.5432"
    2018-11-05 15:02:53.460 KST [41569] LOG:  database system was shut down at 2018-11-05 15:02:32 KST
    2018-11-05 15:02:53.465 KST [41568] LOG:  database system is ready to accept connections
    done
    server started
    </code>

psql postgres

</pre>

## 2. createUser 수정

<pre>
<code>
const createUser = (request, response) => {
  const { name, email } = request.body

  pool.query('INSERT INTO users (name, email) VALUES ($1, $2) RETURNING id', [name, email], (error, results) => {
    if (error) {
      throw error
    }
    response.status(201).send(`User added with ID: ${results.rows[0].id}`)
  })
}
</code>
</pre>