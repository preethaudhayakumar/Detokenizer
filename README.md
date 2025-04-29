# Detokenizer
To recover sub-strings from original string that map to the tokens classified as positive labels

1. Requirement
    
        a. To recover sub-strings from original string that map to the tokens classified as positive labels
    
2. Assumptions & Takeaway
    
        a. Given: xlm - Roberta tokenizer 
        b. Since, Roberta tokenizer supports 100+ languages, here its devloped & validated against English alone.
        c. Since, I'm free to use any resources, I used XLM Roberta Fast tokenizer, which provides the feature
           called offset mapping, that allows users to map each token back to its original input string. 
        d. Disabled special tokens like .. to avoid unnecessary things
            
3. Notebook Flow
            
        3.1 Definition of needed packages
        3.2 Implementation of TextProcessor class
        3.3 Implementation of Front-End
        3.4 Demo video of how to use

2. Developemnt's Environment setup
            
        a. Hardware - Macbook M1
        b. Software
            - Python = 3.9.18v
            - transformers = 4.45.2v
            - gradio(front-end) = 4.44.1v
    
4. Validation
            
        a. Functional testing: Created different test cases: border-cases, best-cases & worst-cases as follow,
            - Case 1:If all the labels are positive, "extract sub-string" should return entire string
            - Case 2:If all the labels are zeros, "extract sub-string" should return null.
            - Case 3:Created multiple toy examples with special characters, wrong spellings and spacings.
                    
                       Eg. "How a re you   ddDoing !#" 

                       It was observed that for the combination of wrong spellings and wrong spacings,
                       offset_mapping did mess up one time. I explored in that direction, but it complicates the
                       code simiplicity.
            
        b. Unit testing of the functions
            - Like "Mis-match should be thrown when len(tokens) != len(labels)"
            
5. Approach summary
            
        - Tokenize the raw string with xlm-roberta while setting return_offsets_mapping=True to get character 
          spans for each token.
        - Use the token offset mapping to extract the corresponding character spans in the input string.
