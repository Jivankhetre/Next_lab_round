# Next_lab_round


I have uploaded the python codes for 3 questions in the gitlab repo. For question 2 which requires deploying on streamlink, I have done that and will be sharing the live link below

**#Question 1:
Write a regex to extract all the numbers with orange color background from the below text in italics.**


{"orders":[{"id":1},{"id":2},{"id":3},{"id":4},{"id":5},{"id":6},{"id":7},{"id":8},{"id":9},{"id":10},{"id":11},{"id":648},{"id":649},{"id":650},{"id":651},{"id":652},{"id":653}],"errors":[{"code":3,"message":"[PHP Warning #2] count(): Parameter must be an array or an object that implements Countable (153)"}]}

Answer: The code does the same. I used regex along with checking the condition that the digits need to begin with a :


**#Question 2:**
**From chrome reviews, goal is to identify such ratings where review text is good, but rating is negative- so that the support team can point this to users. Deploy it using - Flask/Streamlit etc and share the live link.**


Answer: I have shared the code here in gitlab. The datasets used is the same which was provided. The overall idea is as follows. 
    1. Read data from csv using pandas
    2. Extract useful columns
    3. Convert rating to a positivity score - which denotes the class to which it belongs to. Rating of above 3 is classified as 1, other ratings as 0.
    4. Use NLP tools to learn semantics of the review texts - we cannot evaluate the reviews without understanding the semantics.. We need to find the correlation between a good rating and usage of positive words in the reviews like good app, nice etc. For this we used NLTK which helped in cleaning the data and creating a corpus of useful words. Each review form the data point and column entries are all possible words with 0s if not a part of the text and 1s if part of the text.  
    5. Then, we train the model using random forests.. we do not want to overfit the model as there is a chance that a good review can have a bad rating. Finally we validate using test data, but wouldn't go back to fine tune the model, as we are expecting erroneous classification from the original data in small proportions. 
    6. We are looking for those rows where the semantic analysis gives rating 1, while the review rating positivity is 0 - extract these rows and display
    7. Put all of this into streamlit and accept inputs from a csv as test data

_**Regarding the output**_: we have found that there are many entries in the output where there are bad reviews accompanied by bad ratings. This shouldn't have been counted however. The reason for this observation was that the training data was limited and as a result there was some limitations for ex, on max_features for vectorizer. 
On the positive side, there are many bad ratings with good reviews also present in the output.


The streamlit live link for deployed app is https://share.streamlit.io/jivankhetre/next_lab_round/main/deploy_chrome_review.py
(An error message pops up when waiting for the file to be uploaded. It is not a technical error but a minor one which does not affect the performance in anyway)


**#Question 3: Ranking Data - Understanding the co-relation between keyword rankings with description or any other attribute.**

Answer: Owing to shortage of time, I was unable to develop a functioning model which would experimentally answer these questions. I will make an attempt to answer it here theoretically.
 - Ranking has direct correlation to the keyword used in search and presence of that keyword in either the app_id directly or in the app description. 
 - Early presence of keyword will impact the ranking as even with humans we see that people tend to look for catch words in the initial couple of sentences.
 - APP ID has direct impact on the ranking as the search keyword, if present in the app_id itself, will impact in improving the ranking of the app in playstore.
 - Another parameter that would affect the ranking is how many times an user who is looking out for a particular functionality chooses to press the app link. That is determined by the type of catchy adjectives used to explain about the in the short description. Like easy to use, free to use, etc.
 - Short description will be more catchy if they are precise, than long descriptions

 **Part Two:**
**Question: Please use any pre-trained model or use text from open datasets. Once done, please evaluate the English Grammar in the text column of the below dataset**

 Answer: 
 I have used pretrained language-tool for performing the grammar check. I have used the language_tool_python wrapper for the well-known Java LanguageTool. I accept the input as pandas dataframe and keep only the review text column, and pass this text one by one to the language tool to evaluate the grammatical correctness. If there are no mistakes - we print no mistakes, else the number of mistakes detected would be printed.
 - Prerequisites to run the code - Python 3.6+ & LanguageTool (Java 8.0 or higher)

**Sample output:**
- Tony bahut funny hai Hill climbing racing my favourite game  -- Mistakes found,  3  mistakes 
- Teturwu  -- Mistakes found,  1  mistakes

**#Question: Write about any difficult problem that you solved.**

Ans: I had been working on the project Customer churn analysis, which i found difficult because using the machine learning models for the
prediction about the customer was not easy. i have to go through the data set which was about the telecom industry, many times looking into data for various relation co-relation.
and doing full EDA. Full EDA was the part which took a lots of time. After doing that model building was nexty step. This was a good accomplishment considering the problem at hand. 

**#Q2. Ordered pairs of real numbers (a,b) a,b∈R form a vector space V. Which of the following is a subspace of V?**
•	The set of pairs (a, a + 1) for all real a
•	The set of pairs (a, b) for all real a ≥ b
•	The set of pairs (a, 2a) for all real a
•	The set of pairs (a, b) for all non-negative real a,b

Ans: For a subspace H to be a vector space by itself, it has to fulfil the following 3 criteria.
(i)	Zero - The zero vector of vector space V must also be in H
(ii)	Addition - For each u,v in H, u+v is also in H.
(iii)	Scalar multiplication - For each u in H and a scalar c, cu is also in H.
Let us consider each of the above sets and discuss whether they form a subspace of V
•	The set of pairs (a, a + 1) for all real a
-	clearly (0,0) which is the zero of vector space V is not in this set. So it can’t be a subspace

•	The set of pairs (a, b) for all real a ≥ b
-	It meets the first two criteria discussed above. It has the zero vector (0,0) in it. It also satisfies the addition rule. But it fails to meet the scalar multiplication rule. Ex: let c = -5, u = (4,3) cu = (-20,-15) which is not an element of the given set.

•	**The set of pairs (a, 2a) for all real a**
-	It meets all the 3 criteria. It has the zero vector (0,0) in it. It meets the addition rule. Ex: for any u = (a,2a) and v = (b,2b), u+v = (a+b, 2(a+b)) which belongs to the given set. It also meets the scalar multiplication criterion. For any u = (a,2a), cu = (ca, 2ca) which belongs to the given set. So, the set of pairs (a,2a) for all real a, form the subspace of vector space V.

•	The set of pairs (a, b) for all non-negative real a,b
-	It satisfies the first two criteria for being a subspace as it contains both zero vector and satisfies the addition rule for all the elements in the set. But it fails to meet the scalar multiplication criterion, for a choice of negative value for scalar c. ex: if c = -1, an element of the set u = (3,4) , cu = (-3,-4) which is not a member of the given set. 
