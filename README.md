# NLP: BookmarksCleanup Project Phase I

This project is intended to provide a solution to a document *mis*classification problem.\
This common problem can arise from inadequate knowledge about a document, or by usage breakdown.\
 
Usage breakdown occurs when a user (me!) no longer conforms a classification task, self-imposed or not.\
For example, I have quickly bookmarked a web page into a category such as "ML", *while I knew* an \
exisitng category, i.e. "Clustering", or a new-one, "Anomaly Detection" would be more helpful for \
efficient retrieval, which is the main purpose for classification in the first place. \
Thus, this usage breakdown is best examplified by a common fall-back heuristic: "I'll cleanup later". \

Well later is NOW! <br>

This is my first foray into Natural Language Processing and - surprise - I'm liking it!

## Implementation intentions:
Even though the size of my bookmarks 'dataset' is far from astronomical (~30,000 lines), fixing the \
problem misclassification 'by hand' is out of the question. What I want to find is a generative solution:\
an algorithm that will propose/output a better classification in the form of a folder structure.
	
Before claiming a general solution, I want to fix a more narrow problem: How to cleanup my Chrome \
browser bookmarks? In other words, how to 're-classified' my Chrome browser bookmarks into the \
exisitng subgroups I have created, or into new ones if necessary? \
With a few modifications, the solution can be extended to cleanup one's misclassified Internet 
Explorer Favorites folders or a library of *meaningfully* titled files, in case the 'minimal \
implementation' (described further down), is sufficient.

## Raw input: Chrome Bookmarks file

> Note: the current bookmarks.json file in the project ./data folder holds dummy data for privacy reasons.

Chrome holds a user's bookmarks in three folders whose subfolders are called children:
  a. Bookmarks bar
  b. Other bookmarks
  c. Mobile bookmarks

The "Bookmarks bar" and "Mobile bookmarks" folders will not be used as I have not created any \
subcategories/subfolders in them.\
Thus, this project is restricted to finding a solution to the misclassification of bookmarks in the \
"Other bookmarks" subfolder, at least initially. I anticipate that a useful extension of the found \
solution - if any, the "Mobile bookmarks" will be able to 'correctly' merge them into the (cleaned up)\
"Other bookmarks" folder.

This is the json format of a bookmark item:
```
{
    "date_added": "13109116258863484",
    "id": "498",
    "meta_info": { "last_visited_desktop": "13169489896848926"},
    "name": "Wik",
    "sync_transaction_version": "779",
    "type": "url",
    "url": "http://en.wikipedia.org/wiki/Main_Page"
}

There are at least, two fields I will not use as features: "id" and "sync_transaction_version"; \
"type" may be the third one if my "minimal implementation" (below) works.\

Features pre-processing to do:
+ Un-nest the "last_visited_desktop" dictionary item
+ Create a "location" feature = concatenated parent folder name(s)
+ Words vector: for "location", "name" and "url"

Input model structure (flatten vector):
` bookmark_i:  date_added | last_visited_desktop | word_vect\


### These are the steps in my workflow:

First, I will try an implementation (A) that does not rely on web scrapping the pages given by the \
urls. This might work as I (often) rename the bookmark with a more descriptive label. This is a big \
'if', but if this works, then extending this reclassification project to any library by only using \
its documents titles may also be possible...Tests will tell!\

The difference between these two implementations resides 
Phase I:

##A. Minimal implementation:
### 1. Process Chrome bookmarks file
> [Progress workbook](https://github.com/Sylatac/NLP_ChromeBookmarksCleanup_Project_PhaseI/blob/master/Bookmarks_Phase_I.ipynb)
### 2. Define 'good enough outcome' and ways to test it
### 3. Apply some classification algorithms on the output of Step 1
### 4. Evaluate on path-labeled and path_unlabeled data (for comparison with new classification)
### 5. Create a cleaned up Bookmarks file

Phase II:
##B. Extended implementation (additional processing):
### 1. Process Chrome bookmarks file
### => To include web scraping data into word vector


PS: The markdown line break character, "\" (backslash) has a stochastic behavior: it sometimes\
works...
