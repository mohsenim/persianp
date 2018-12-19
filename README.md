## Persianp Processing Toolbox

Persianp is a text processing tool developed in Java to preprocessing Persian texts. The toolbox accomplishes following tasks:
* Character-level normalization
* Tokenization
* Lemmatization
* POS tagging
* Stopword detection
* Noun phrase chunking

### Using Persianp from the command line
Be sure folder `res` is next to the `jar` file.

```bash
$ java -cp persianp-toolbox-1.0.jar com.persianp.nlp.process.Process -input inputfile.txt -output outputfile.txt -task (tokenize|tag|lemmatize|taglemmatize) [-nostopword] [-prop propertyFile.properties]
```

At the moment NP chunking is not supported from the comand line.

### Using the Persianp API
Add the API to libraries of your program. The following example shows how to use the toolbox.

```
public class TestPersianp { 

    public static void main(String[] args) { 
        TestPersianp testPersianp = new TestPersianp(); 
        testPersianp.process(); 
    } 

    private void process() { 
        try { 
            Properties properties = new Properties(); 
            properties.load(this.getClass().getClassLoader().getResourceAsStream("persianp.properties"));
            Process process = new Process(properties); 
            InputStream in = this.getClass().getClassLoader().getResourceAsStream("testText.txt");
            BufferedReader br = new BufferedReader(new InputStreamReader(in, "UTF-8"));
            String line; 
            while ((line = br.readLine()) != null) { 
                process.process(line); 

                System.out.println(process.getText()); 
//                process.getTokens(); 
//                process.getTokensText(); 
//                process.getTags(); 
//                process.getChunkTag(); 
//                process.getLemmas(); 
//                process.getNonStopwordTokens(); 

                int sentenceSize = process.getSentencesSize(); 
                for (int j = 0; j < sentenceSize; ++j) { 
//                    List tokensText = process.getTokensTextInSentence(j); 
//                    List tags = process.getTagsInSentence(j); 
//                    List lemmas = process.getLemmasInSentence(j); 
                    List tokens = process.getTokensInSentence(j); 
                    for (int k = 0; k < tokens.size(); ++k) { 
                        System.out.println(tokens.get(k).getText() + "\t\t\t" + tokens.get(k).getLemma() + "\t\t\t" + tokens.get(k).getTag());
                    } 
                } 
            } 
            in.close(); 
            br.close(); 
        } catch (Exception e){ 
            e.printStackTrace(); 
        } 
    } 
} 

```

### More Information / Citing This Toolbox
Please cite the paper below if you use the Persianp toolbox in your research. It also provides more information about the toolbox.

> Mahdi Mohseni, Javad Ghofrani, and Heshaam Faili.
> "Persianp: A Persian Text Processing Toolbox".
> International Conference on Intelligent Text Processing and Computational Linguistics
CICLing 2016: Computational Linguistics and Intelligent Text Processing, pp 75-87.

Bibtex citation:

```
@InProceedings{Persianp2016,
author="Mohseni, Mahdi
and Ghofrani, Javad
and Faili, Heshaam",
title="Persianp: A Persian Text Processing Toolbox",
booktitle="Computational Linguistics and Intelligent Text Processing",
year="2018",
publisher="Springer International Publishing",
pages="75--87",
isbn="978-3-319-75477-2"
}
```
