l10n_br_core
============

[![Build Status](https://travis-ci.org/openerpbrasil/l10n_br_core.png?branch=7.0)](https://travis-ci.org/openerpbrasil/l10n_br_core)

Goal
----

Este projeto contêm os principais módulos da localização brasileira do OpenERP, estes módulos são a base dos recursos

* Fiscais
* Contábil
* Sped

Sobre
-----

Este projeto é open source sobre licença AGPL v3 http://www.gnu.org/licenses/agpl-3.0.html

Esse projeto [segue se aperfeiçoando desde o inicio de 2009](https://github.com/openerpbrasil/l10n_br_core/network). O código era [inicialmente desenvolvido no Launchpad](https://code.launchpad.net/openerp.pt-br-localiz) mas segue agora no Github (ainda que [com espelho Launchpad](https://code.launchpad.net/~openerp-brazil-core-team/openerp.pt-br-localiz/l10n_br_core-7.0)). Se trata de um projeto aberto, meritocratico, sob a liderança da [Akretion](http://www.akretion.com/) (gold partner OpenERP; >90% dos commits do projeto, membro co-fundador da organização OpenERP Community Assoctiation - OCA http://openerp-community-association.org), e com a ajuda de vários outros contribuidores queridos listados aqui https://github.com/openerpbrasil/l10n_br_core/graphs/contributors

Alem de desenvolver as funcionalidades, os professionais por trás desse projeto interagem com o core do projeto OpenERP para propor melhorias para que a localização se integra da forma mais suave possível mesmo que o OpenERP não foi inicialmente projetado para o mercado brasileiro pela editora Belga OpenERP SA. Assim já foram assim dezenas de “merge proposals” melhorando a modularidade em geral do OpenERP que foram integrada no core do OpenERP graça a esse projeto.

Non goal
--------

* extender ou modificar as funcionalidades do OpenERP não vinculadas à localização brasileira. Outros módulos em outros projetos são perfeitos para isso.
* de uma forma geral, re-implementar aqui o que ferramentas terceiras já fazem bem.
* quando há razoavelmente varias soluções técnicas para resolver um problema, o projeto do core da localização não quer impor uma dependência importante. Outros módulos e projetos são bem vindos nesse caso.
* implementar o PAF-ECF no PDV web do OpenERP. Se trata de um trabalho muito burocrático que ia requerer de modificar muito o PDV do OpenERP enquanto se conectar com PDV’s do mercado é uma alternativa razoável.
* manter dados para a folha de pagamento legal no Brasil
* ter a responsabilidade manter dados fiscais em geral. Em geral esse tipo de serviço requer uma responsabilidade jurídica que se negocia caso a caso.

Aviso - “As proezas deste filme são realizadas por profissionais”
-----------------------------------------------------------------

Apesar do OpenERP ser relativamente fácil de baixar para brincar, implementar um ERP (e não apenas um software de banca de jornal) já não é fácil. Mas aqui se trata então de um ERP de código aberto que apesar de ter um bom framework para um ERP não é um produto pronto assim como um ERP proprietário com milhões de investimento ou décadas de mercado, ainda menos aqui no Brasil. Alem de metodologia de implementação de ERP, é preciso de bastante conhecimentos contábeis e fiscais e ainda de alta capacitação técnica como programador (“eu ja fiz um site em PHP” não basta).

Ou seja, os autores desse projeto, investem diariamente para democratizar o OpenERP melhorando-lo, mas não apóiam a demagogia de deixar pensar que pessoas não extremamente bem preparadas vão se dar bem implementando o OpenERP em casa por conta própria. Seria um pouco como você querer re-escrever o driver Linux da sua placa wifi ou construir um carro no seu quintal a partir de planos que você baixou da Internet para pegar um exemplo. Algumas pessoas tem disposição para esse tipo de desafio, mas é melhor ser bem lucido e criterioso na escolha.

Instalação
----------

Instalar o OpenERP para produção foge um pouco do scope desse projeto. Pois é algo complexo, em evolução, e que varia muito dependendo se você quer apenas testar, desenvolver, usar em produção ou ainda hospedar.

Vamos então dar aqui os procedimentos simples para testar apenas o core da localização brasileira do OpenERP numa maquina Ubuntu. Mas deixamos claro que essa forma de instalar certamente não é adequada para produção em termo de segurança, desempenho e mantenabilidade.

```
# pacotes debian:
sudo apt-get install postgresql-server
sudo apt-get install -qq graphviz
sudo apt-get -ym install python-dateutil python-docutils python-feedparser python-gdata python-jinja2 python-ldap python-lxml python-mako python-mock python-openid python-psycopg2 python-psutil python-pybabel python-pychart python-pydot python-pyparsing python-reportlab python-simplejson python-tz python-unittest2 python-vatnumber python-vobject python-webdav python-werkzeug python-xlwt python-yaml python-zsi python-imaging bzr

# OpenERP v7.0 nightly:
wget http://nightly.openerp.com/7.0/nightly/src/openerp-7.0-latest.tar.gz
mkdir -p src
tar -xf openerp-7.0-latest.tar.gz -C src

for f in ./src/*
do
    echo "$f" | grep -Eq '^\./abc.[0-9]+$' && continue
    echo "Something with $f here"
done

mv $f openerp
rm -rf ./src
cd openerp
python setup.py --quiet install
cd ..

# dependencias para as regras fiscais:
bzr branch --stacked lp:openerp-fiscal-rules fiscal_rules

# codigo do projeto l10n_br_core (esse projeto):
git clone https://github.com/openerpbrasil/l10n_br_core.git --depth=1 --branch=7.0


psql -c "CREATE USER openerp WITH PASSWORD 'admin';" -U postgres
psql -c 'create database l10n_br_test with owner openerp;' -U postgres


# serviço OpenERP:
cd openerp
./openerp-server --db_user=postgres --db_user=openerp --db_password=admin --db_host=localhost --stop-after-init --addons-path=../fiscal_rules,../l10n_br_core
```

Depois como usuário admin (senha admin), instalar os módulos l10n_br_**

E aconselhado instalar os módulos conforme a necessidade e capacidade de implementação, aos poucos e não todos módulos de uma só vez. Instalar com dados de demostração ajuda a avaliar os módulos melhor.

Contribuindo com codigo
-----------------------

Você pode resolver umas das issues cadastradas no Github ou implementar melhorias em geral, enviando-nos um pull request com as suas alterações.

lista de discussão: http://www.openerpbrasil.org/comunidade



