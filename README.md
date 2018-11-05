# node-api-postgres
Node Express Posgresql

##brew install postgresql

##brew services stop postgresql

##pg_ctl -D /usr/local/var/postgres start

waiting for server to start....2018-11-05 15:02:53.444 KST [41568] LOG:  listening on IPv6 address "::1", port 5432
2018-11-05 15:02:53.444 KST [41568] LOG:  listening on IPv4 address "127.0.0.1", port 5432
2018-11-05 15:02:53.445 KST [41568] LOG:  listening on Unix socket "/tmp/.s.PGSQL.5432"
2018-11-05 15:02:53.460 KST [41569] LOG:  database system was shut down at 2018-11-05 15:02:32 KST
2018-11-05 15:02:53.465 KST [41568] LOG:  database system is ready to accept connections
 done
server started

##psql postgres



const createUser = (request, response) => {
  const { name, email } = request.body

  pool.query('INSERT INTO users (name, email) VALUES ($1, $2) RETURNING id', [name, email], (error, results) => {
    if (error) {
      throw error
    }
    response.status(201).send(`User added with ID: ${results.rows[0].id}`)
  })
}

