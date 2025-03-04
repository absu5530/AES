# AUTOMATED ESSAY SCORER

Automated essay scorers are used by a number of testing services in order to reduce the dependency on human resources in the grading process. Standardized tests, which are taken by large numbers of people and tend to have a predetermined and consistent format are especially suitable for this type of technology.

Education Testing Service (ETS) is perhaps the most well-known of these testing services, and it uses a trademark 'e-rater' technology to grade the Analytical Writing Measure of the Graduate Record Examinations (GRE). According to ETS, this technology extracts certain features representative of writing quality that not only predict scores accurately, but also have a 'logical correspondence to the features that readers are instructed to consider when they award scores'. The score for every GRE essay is the average of the scores of one human grader and the scoring engine; if these two scores differ by more than one point (out of six), the essay is scored by another human grader and that score is used to compute the average instead of the scoring engine's score. The features currently included in the scoring engine are:

- content analysis based on vocabulary measures
- lexical complexity/diction
- proportion of grammar errors
- proportion of usage errors
- proportion of mechanics errors
- proportion of style comments
- organization and development scores
- features rewarding idiomatic phraseology

The goal of this project is to implement a scoring algorithm based on this method using linear SVM and as many of these features as possible to try and see what accuracy can be reached.

There is a large data set of graded essays that was uploaded onto the predictive modeling and analytics platform Kaggle by the William Flora Hewlett Foundation about six years ago as part of a competition to find the best automated scoring algorithm. The data consists of eight essay sets with between 1000-3000 essays in each set, and the rubrics for grading the essays. Each essay is about 100-550 words long. Some of the essays are more dependent on a particular source text than others, and the rubrics reflect this in their grade brackets. The data for each essay set consists of the essays themselves, one or more scores for each essay (the score ranges are different across the essay sets) and a resolved score if there is more than one score. This is the data that will be used to train this essay grader algorithm. The input data for the grader would be entire essays (and their corresponding question prompts) and the output would be scores.

Because the data set consists of vastly different essay sets with different scoring bands and rubrics, only two of these essay sets that have similar scoring bands (0-4) are being used for the purposes of this project. A representation of the classification output as a confusion matrix is given.

## Findings

The accuracy of the algorithm is 62%. The confusion matrix shows that most essays were either rated accurately or very close to the gold class, which is a good result. With essays rated on a six-point scale like on the GRE we might see a somewhat lower lenient accuracy (such data is not available in this data set), but it would nevertheless be quite high.

During the process of feature engineering, using only basic text metrics such as word count and sentence length in the classifier seemed to make the classifier perform slightly better than chance. It was the POS tags and tf-idf scores that boosted the accuracy significantly. The fact that a high lenient accuracy was obtained, going by the GRE scoring method, shows that to some extent automated essay scoring can be done quite successfully just with features such as the ones used here that act as proxies for semantic difficulty and syntactic complexity, without any regard for the actual analytical merit of the essay.

Of course, the limited diversity of data poses a key problem here. It is inevitable that this classifier picked up on features specific to the two essay prompts used in the input. It would be ideal to use essays graded on the same scale from a range of different topics and answering a range of different questions to train the algorithm. This might yield a better trained classifier that would be more attuned to good writing regardless of subject matter, and would be a good improvement on this work if such data could be found.
