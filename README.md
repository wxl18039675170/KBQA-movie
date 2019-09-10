# KBQA-movie
   Before starting, you need download d2rq-0.8.1, apache-jena-3.12.0 and apache-jena-fuseki-3.12.0, and put those files to our project root path.
# 1. Data
        1. ./data/kg-demo_movie.sql
        2. download from "https://link.zhihu.com/?target=https%3A//www.themoviedb.org/'
        
# 2. Create RDF
        
        1. cd d2re-0.8.1
        2. ./generate-mapping -o movie_mapping.ttl -u root -p Philips@1 jdbc:mysql://localhost:3305/kg_demo_movie?useSSL=false&useUnicode=true&characterEncoding=utf8
        3. ./dump-rdf -o ./demo_movie.nt ./movie_mapping.ttl
        
#3. Load RDF to fuseki server

        1. cd apache-jena-3.12.0/bin
        2. ./tdbloader apache-jena-fuseki-3.12.0/tdb d2rq-0.8.1/demo_movie.nt
        
#4. Start fuseki server

        1. cd apache-jena-fuseki-3.12.0    
        2. ./fuseki-server 
        3. stop sever(ctr+c), you will "run" and  file, cd ./run
        4. put fuseki_conf.ttl to configration. put ontology.ttl and rules.ttl to database
        5. cd ..
        6. cd ./fuseki-server
        7. open your Chrome, go http://localhost:3030
        
#5. Notes about config and database

        1. fuseki_conf.ttl,  you can config reasonerURL which is OWLFBRuleReasoner or GenericRuleReasoner. Dont' keep both reasoner.
        2. don't set ontology.ttl at config file. maybe you can't start fuseki server. please start server, open http://localhost:3030 and add database.
        3. RDF data must match your ontology
        