# Translate Text

In this article you will learn how to translate a text using APIs.

## Translate

<Tabs>

<TabItem value="api" label="API">

Pass your text in the `text` attribute and set `sourceLanguage` and `targetLanguage` using the language codes mentioned in Language Support below.

```bash title="Translate API"
curl --location --request POST '{API_LINK}' \
--header 'Accept: application/json, text/plain, */*' \
--header "authorization: ${AUTHORIZATION_TOKEN}" \
--header 'Content-Type: application/json;charset=UTF-8' \
--data-raw '{
    "text": "I work at Lingy",
    "sourceLanguage":"en",
    "targetLanguage": "hi"}'
```


</TabItem>
</Tabs>


## Translate Text with Entities

When you translate a sentence with annotations, like entities, 
you loose the annotations in the translated text as the words get rearranged and it is hard to find which phrase in the translated text corresponds to which entity in the source language text.

This is exactly why we have this API. You can pass entity annotations to our translation API and preserve these annotations in the translated text too.

<Tabs>
<TabItem value="api" label="API">

Pass your text in the `text` attribute and set `sourceLanguage` and `targetLanguage` using the language codes mentioned in Language Support. 
`entities` are the annotations you want to preserve in the translated text. 
Entities have to have a `start` and an `end` character index denoting where in the text they occur. Additionally, each entity should have a `value` attribute which should contain the exact entity value, and an `entity` attribute denoting the type of entity it is.  

```bash title="Translate with Entities API"
curl --location --request POST '{API_LINK}' \
--header 'Accept: application/json, text/plain, */*' \
--header "authorization: ${AUTHORIZATION_TOKEN}" \
--header 'Content-Type: application/json' \
--data-raw '{
    "text": "राजस्थान के करौली शहर में हिंदू नववर्ष के मौके पर हिंदुओं ने 2 अप्रैल को एक बाइक रैली निकाली थी।",
    "sourceLanguage": "hi",
    "targetLanguage": "en",
    "entities": [
            {
                "start": 61,
                "end": 62,
                "value": "2",
                "entity": "cardinal"
            },
            {
                "start": 73,
                "end": 75,
                "value": "एक",
                "entity": "cardinal"
            },
            {
                "value": "राजस्थान",
                "start": 0,
                "end": 8,
                "entity": "location"
            },
            {
                "value": "करौली",
                "start": 12,
                "end": 17,
                "entity": "location"
            }
        ]
}'
```

</TabItem>
</Tabs>


The response object looks something like the following. Note that the entities are preserved in the translated output. 

```json
{
    "success": true,
    "message": "Data fetched succssfully",
    "data": {
        "text": "राजस्थान के करौली शहर में हिंदू नववर्ष के मौके पर हिंदुओं ने 2 अप्रैल को एक बाइक रैली निकाली थी।",
        "translatedText": "On the occasion of Hindu New Year in Karauli city of Rajasthan Hindus took out a a bike rally on 2 April.",
        "suggestions": [
            "On the occasion of Hindu New Year in Karauli city of Rajasthan Hindus took out a a bike rally on 2 April."
        ],
        "entities": [
            {
                "start": 37,
                "end": 44,
                "value": "Karauli",
                "entity": "location"
            },
            {
                "start": 53,
                "end": 62,
                "value": "Rajasthan",
                "entity": "location"
            },
            {
                "start": 10,
                "end": 11,
                "value": "a",
                "entity": "cardinal"
            },
            {
                "start": 97,
                "end": 98,
                "value": "2",
                "entity": "cardinal"
            }
        ]
    }
}
```

## Language Support

For translation, we currently support **108 languages**. All APIs accept language codes in the following tables based on the region of the language.

### 👉 Indian Subcontinent 
| Language &emsp;&emsp;&emsp;&emsp;&emsp; |`code`| Language&emsp;&emsp;&emsp;&emsp;&emsp;|`code`| Language &emsp;&emsp;&emsp;&emsp;&emsp;|`code`|
| ------------------------------- | ------------: | --------------------------------| ------------: | ---------------------------------| ------------: |
| Assamese                        | `as`          | Bengali                         | `bn`          | Gujarati                         | `gu`          |
| Hindi                           | `hi`          | Kannada                         | `kn`          | Malayalam                        | `ml`          |
| Marathi                         | `mr`          | Nepali                          | `ne`          | Odia (Oriya)                     | `or`          |
| Punjabi                         | `pa`          | Sindhi                          | `sd`          | Sinhala (Sinhalese)              | `si`          | 
|Tamil                             | `ta`          | Telugu                          | `te`          |  Urdu                            | `ur`          |   

### 👉 South-East Asia
| Language &emsp;&emsp;&emsp;&emsp;&emsp; |`code`| Language&emsp;&emsp;&emsp;&emsp;&emsp;|`code`| Language &emsp;&emsp;&emsp;&emsp;&emsp;|`code`|
| ------------------------------- | ------------: | --------------------------------| ------------: | ---------------------------------| ------------: |
|Burmese (Myanmar)|`my` |Cebuano           |`ceb`|Dhivehi  |`dv`|
|Hmong            |`hmn`|Indonesian        |`id` |Javanese |`jv`|
|Khmer            |`km` |Malay             |`ms` |Loa      |`lo`|
|Sundanese        |`su` |Tagalog (Filipino)|`tl` |Thai     |`th`|
|Urdu             |`ur` |Vietnamese        |`vi` |         |    |


### 👉 Middle-East Asia Northern Africa (MENA)
| Language &emsp;&emsp;&emsp;&emsp;&emsp; |`code`| Language&emsp;&emsp;&emsp;&emsp;&emsp;|`code`| Language &emsp;&emsp;&emsp;&emsp;&emsp;|`code`|
| ------------------------------- | ------------: | --------------------------------| ------------: | ---------------------------------| ------------: |
| Arabic                          | `ar`          | Hebrew                          | `he`          | Pashto                           | `ps`          |
| Persian                         | `fa`          | Uighur                          | `ug`          | Turkmen                          | `tk`          |

### 👉 Rest-of-Asia
| Language &emsp;&emsp;&emsp;&emsp;&emsp; |`code`| Language&emsp;&emsp;&emsp;&emsp;&emsp;|`code`| Language &emsp;&emsp;&emsp;&emsp;&emsp;|`code`|
| ------------------------------- | ------------: | --------------------------------| ------------: | ---------------------------------| ------------: |
|Armenian|`hy`|Azerbaijani|`az`|Chinese (Simplified)|`zh-CN`|
|Chinese (Traditional)|`zh-TW`|Georgian |`ka`|Japanese |`ja`|
|Kazakh  |`kk`|Kirghiz    |`ky`|Korean              |`ko`   |
|Kurdish |`ku`|Kyrgyz     |`ky`|Mongolian           |`mn`   |
|Russian |`ru`|Tagalog    |`tl`|Tajik               |`tg`   |
|Tatar   |`tt`|Uzbek      |`uz`|                    |       |


### 👉 Africa
| Language &emsp;&emsp;&emsp;&emsp;&emsp; |`code`| Language&emsp;&emsp;&emsp;&emsp;&emsp;|`code`| Language &emsp;&emsp;&emsp;&emsp;&emsp;|`code`|
| ------------------------------- | ------------: | --------------------------------| ------------: | ---------------------------------| ------------: |
| Afrikaans     | `af` | Amharic          | `am` | Bambara          | `bm`          |
| English       | `en` | French           | `fr` | Hausa            | `ha`          | 
| Igbo          | `ig` | Kinyarwanda      | `rw` | Lingala          | `ln`          | 
| Malagasy      | `mg` | Nyanja (Chichewa)| `ny` | Oromo            | `om`          |
| Sesotho       | `st` | Shona            | `sh` | Somali           | `so`          |
| Swahili       | `sw` | Tigrinya         | `ti` | Tsonga           | `ts`          | 
| Twi           | `tw` | Xhosa            | `xh` | Yoruba           | `yo`          |
| Zulu          | `zu` |                  |      |                  |               |

### 👉 Europe 
| Language &emsp;&emsp;&emsp;&emsp;&emsp; |`code`| Language&emsp;&emsp;&emsp;&emsp;&emsp;|`code`| Language &emsp;&emsp;&emsp;&emsp;&emsp;|`code`|
| ------------------------------- | ------------: | --------------------------------| ------------: | ---------------------------------| ------------: |
| Albanian                        | `sq`          | Aragonese                       | `an`          | Bashkir                         | `ba`          |
| Basque                          | `eu`          | Belarusian                      | `be`          | Bosnian                         | `bs`          |
| Breton                          | `br`          | Bulgarian                       | `bg`          | Catalan                         | `ca`          |
| Chechen                         | `ce`          | Chuvash                         | `cv`          | Corsican                        | `co`          |
| Croatian                        | `hr`          | Czech                           | `cs`          | Danish                          | `da`          | 
| Dutch                           | `nl`          | English                         | `en`          | Esperanto                       | `eo`          |
| Estonian                        | `et`          | Finnish                         | `fi`          | French                          | `fr`          |
| Frisian                         | `fy`          | Galician                        | `gl`          | German                          | `de`          |
| Greek                           | `el`          | Hungarian                       | `hu`          | Icelandic                       | `is`          |
| Irish                           | `ga`          | Italian                         | `it`          | Latin                           | `la`          |
| Latvian                         | `lv`          | Lithuanian                      | `lt`          | Luxembourgish                   | `lb`          |
| Macedonian                      | `mk`          | Maltese                         | `mt`          | Norwegian Bokmål                | `nb`          |
| Occitan                         | `oc`          | Polish                          | `pl`          | Portuguese                      | `pt`          |
| Romanian                        | `ro`          | Scots Gaelic                    | `gd`          | Serbian                         | `sr`          |  
| Slovak                          | `sk`          | Slovenian                       | `sl`          | Spanish                         | `es`          |
| Swedish                         | `sv`          | Turkish                         | `tr`          | Ukrainian                       | `uk`          |
| Welsh                           | `cy`          | Yiddish                         | `yi`          |                                 |               |

### 👉 North-South America
| Language &emsp;&emsp;&emsp;&emsp;&emsp; |`code`| Language&emsp;&emsp;&emsp;&emsp;&emsp;|`code`| Language &emsp;&emsp;&emsp;&emsp;&emsp;|`code`|
| ------------------------------- | ------------: | --------------------------------| ------------: | ---------------------------------| ------------: |
| Aymara        |`ay` | Dutch     |`nl`| English      |`en`| 
| French        |`fr` | Guarani   |`gn`| Haitian      |`ht`| 
| Hawaiian      |`haw`| Portuguese|`pt`| Quechua      |`qu`| 
| Samoan        |`sm` | Spanish   |`es`| Yiddish      |`yi`|

### 👉 Australia/New-Zealand
| Language &emsp;&emsp;&emsp;&emsp;&emsp; |`code`| Language&emsp;&emsp;&emsp;&emsp;&emsp;|`code`| Language &emsp;&emsp;&emsp;&emsp;&emsp;|`code`|
| ------------------------------- | ------------: | --------------------------------| ------------: | ---------------------------------| ------------: |
| English                         | `en`          | Maori                           | `mi`          |
