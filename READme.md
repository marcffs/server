# Servidor

O servidor nao suporta qualquer cabecalho alem da requisicao. Fiz com a porta 8080 pois com a 80 eu precisava usar o **super usuario** e, alem disso, quando criava um arquivo, este sempre se limitava a leitura, pois foi criado como super usuario. Realizei os teste com o telnet e deram certo ambas as requisicoes **GET PUT**. No entanto, para o **PUT**, sao permitidos apenas duas entradas de dados: uma para a requisicao e outra para o conteudo. Assim, o conteudo da requisicao **nao pode ter quebra de linha**. Realizei os testes da seguinte maneira e com o sequinte resultado:

## GET

telnet localhost 8080
Trying 127.0.0.1...
Connected to localhost.
Escape character is '^]'.
GET /kyKiske.html HTTP/1.1
HTTP/1.1 200 OK

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>KY KISKE</title>
    <link rel="stylesheet" href="main.css">
</head>
<body>
    <header>
        <div>ky kiske</div>
    </header>
    <div>
        <h2>normal moves</h2>
        <li>
            <ul>command normal 1: 6p</ul>
            <ul>command normal 2: 6k</ul>
            <ul>command normal 3: 6h</ul>
        </li>
        <h2>special moves</h2>
        <li>
            <ul>stun edge: (air ok) 236s or 236h</ul>
            <ul>stun dipper: 236k</ul>
            <ul>fondre arc: 214k</ul>
            <ul>vapor thrust: (air ok) 623s or 623h</ul>
            <ul>dire eclat: 214s</ul>
        </li>
        <h2>super Moves</h2>
        <li>
            <ul>Tyrant Rave: (costs 50% tension) (air ok) 632146h</ul>
            <ul>Sacred edge: (costs 50% tension) 236236p</ul>
            <ul>Dragon Install: (costs 50% tension) 214214h</ul>
        </li>
    </div>
</body>
</html>
Connection closed by foreign host.

## PUT

telnet localhost 8080
Trying 127.0.0.1...
Connected to localhost.
Escape character is '^]'.
PUT /may.html HTTP/1.1
<!DOCTYPE html><html lang="en"><head><meta charset="UTF-8"><meta name="viewport" content="width=device-width, initial-scale=1.0"><title>MAY</title><link rel="stylesheet" href="main.css"></head><body><header><div>may</div></header><div><h2>normal moves</h2><li><ul>command normal 1: 6p</ul><ul>command normal 2: 6k</ul><ul>command normal 3: 6h</ul></li><h2>special moves</h2><li><ul>mr. dolphin horizontal: [4]6s or [4]6h</ul><ul>mr. dolphin vertical: [2]8s or [2]8h</ul><ul>overhead kiss: 623k</ul><ul>arisugawa sparkle: 214p or 214k</ul></li><h2>super Moves</h2><li><ul>Great Yamada Attack: (costs 50% tension) 236236s</ul><ul>The wonderful and dynamic goshogawara: (costs 50% tension) (air ok) 632146h</ul></li></div></body></html>
HTTP/1.1 201 Created
Content-Location: htdocs/may.html
Connection closed by foreign host.

## SERVER

python3 servidorHTTP.py 
Servidor em execução...
Escutando por conexões na porta 8080
GET /kyKiske.html HTTP/1.1

['GET /kyKiske.html HTTP/1.1\r', '']
PUT /may.html HTTP/1.1

['PUT /may.html HTTP/1.1\r', '']
<!DOCTYPE html><html lang="en"><head><meta charset="UTF-8"><meta name="viewport" content="width=device-width, initial-scale=1.0"><title>MAY</title><link rel="stylesheet" href="main.css"></head><body><header><div>may</div></header><div><h2>normal moves</h2><li><ul>command normal 1: 6p</ul><ul>command normal 2: 6k</ul><ul>command normal 3: 6h</ul></li><h2>special moves</h2><li><ul>mr. dolphin horizontal: [4]6s or [4]6h</ul><ul>mr. dolphin vertical: [2]8s or [2]8h</ul><ul>overhead kiss: 623k</ul><ul>arisugawa sparkle: 214p or 214k</ul></li><h2>super Moves</h2><li><ul>Great Yamada Attack: (costs 50% tension) 236236s</ul><ul>The wonderful and dynamic goshogawara: (costs 50% tension) (air ok) 632146h</ul></li></div></body></html>

## Conclusao

O **GET** consegue arquivos sem problemas e o **PUT** cria arquivos (ou os sobrescreve) contanto que o conteudo nao tenha quebra de linha (secao html em uma linha só). Cheguei a testar no postman tambem, e para o postman funcionou normalmente. No entanto, preferi o telnet pois neste eu tinha que fazer toda a requisicao, enquanto que no postman bastante do processo era automatizado.
