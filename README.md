# BOA Data

this repository contains boa patterns.
boa 10 are the top 10 patterns. 
Boa 100 are the top 100, this comes in 2 parts, a and b. 
inside those *.tar.gz. is the index.

## Usage

First install solr 3.4
```
https://archive.apache.org/dist/lucene/solr/3.4.0/
```

this is the official document for solr 3.4
```
https://lucidworks.com/wp-content/uploads/2011/04/lucidworks-solr-refguide-3.4.pdf
```

then extract boa_en_10.tar.gz in this path
```
solr-3.4.0/example/solr/data/index
```

if the path doesnt exist add an index from the example folder (example/solr/data/index/boa_en) when the folders generate then copy boa index.

## Do query

first run solr from example folder by run 
```
java -jar start.jar
```
by this URL you can visit solr admin page
```
http://localhost:8983/solr/admin/
```
if not it means you didn't run solr correct

for check the index is load correct go to this endpoint

```
http://localhost:8983/solr/select/?q=*%3A*&version=2.2&start=0&rows=10&indent=on
```

if you see the result something like below, it means you index boa successfully
```xml
<response>
<lst name="responseHeader">
<int name="status">0</int>
<int name="QTime">19</int>
<lst name="params">
<str name="start">0</str>
<str name="q">*:*</str>
<str name="rows">10</str>
<str name="indent">on</str>
<str name="version">2.2</str>
</lst>
</lst>
<result name="response" numFound="62728" start="0">
<doc>
<str name="AVERAGE_TOKEN_LENGHT">4.5</str>
<str name="CHARACTER_COUNT">21.0</str>
<str name="COMMA_COUNT">1.0</str>
<str name="DIGIT_COUNT">0.0</str>
<str name="GOOD_PLACE_DOMAIN">0.0</str>
<str name="GOOD_PLACE_RANGE">0.0</str>
<str name="LEVENSHTEIN">1.0</str>
<str name="NNP_COUNT">1.0</str>
<str name="NON_ALPHA_SPACE_COUNT">2.0</str>
<str name="POSSESSIVE">1.0</str>
<str name="POS_REGEX_1">0.0</str>
<str name="POS_REGEX_2">0.0</str>
<str name="POS_REGEX_3">0.0</str>
<str name="REVERB">0.0</str>
<str name="SINGLE_NOUN">0.0</str>
<str name="SPECIFICITY">3.3219280948873626</str>
<str name="SPECIFICITY_OCCURRENCE">1.0</str>
<str name="SUPPORT_NUMBER_OF_MAX_PAIRS_LEARNED_FROM">1.0</str>
<str name="SUPPORT_NUMBER_OF_PAIRS_LEARNED_FROM">1.0</str>
<str name="TF_IDF_IDF">2.4849066497880004</str>
<str name="TF_IDF_TF">12.201013943540822</str>
<str name="TF_IDF_TFIDF">30.318380682460703</str>
<str name="TOKEN_COUNT">4.0</str>
<str name="TOTAL_OCCURRENCE">0.6931471805599453</str>
<str name="TYPICITY">0.34657359027997264</str>
<str name="TYPICITY_CORRECT_DOMAIN_NUMBER">1.0</str>
<str name="TYPICITY_CORRECT_RANGE_NUMBER">0.0</str>
<str name="TYPICITY_SENTENCES">0.6931471805599453</str>
<str name="UPPERCASE_LETTER_COUNT">1.0</str>
<str name="VERB_COUNT">0.0</str>
<str name="WORDNET_DISTANCE">1.0</str>
<str name="boa-score">0.0</str>
<str name="domain">http://dbpedia.org/ontology/Company</str>
<str name="generalized"/>
<str name="learnedfrom">1</str>
<str name="maxlearnedfrom">1</str>
<str name="nlr-gen">?D? 's _NE_ subsidiary ?R?</str>
<str name="nlr-no-var">'s India subsidiary ,</str>
<str name="nlr-var">?D? 's India subsidiary , ?R?</str>
<str name="pos">POS NNP NN ,</str>
<str name="range">http://dbpedia.org/ontology/Company</str>
<str name="uri">http://dbpedia.org/ontology/subsidiary</str>
</doc>
</result>
</response>
```

for run queries for each field you should change schema.xml in this path
```
solr-3.4.0/example/solr/conf
```

for example if you want do this query 
```
http://localhost:8983/solr/boa_en/select/?q=uri:%22http://dbpedia.org/ontology/award%22
```
you should add this to the config
```
<field name="uri" type="string" indexed="true" stored="true"/>
```

or if you need sort like this
```
http://localhost:8983/solr/boa_en/select/?q=uri:%22http://dbpedia.org/ontology/award%22&sort=SUPPORT_NUMBER_OF_PAIRS_LEARNED_FROM+desc
```
you should add this config
```
<field name="SUPPORT_NUMBER_OF_PAIRS_LEARNED_FROM" type="long" indexed="true" stored="true"/>
```

if the above url generate path not found error then replace 
```
<core name="collections" instanceDir="."/>
```
with 
```
<core name="boa_en" instanceDir="."/>
```
in solr.xml file
