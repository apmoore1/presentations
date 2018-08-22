# Slide 1
Hi thanks for the introduction, today I am going to talk about reproducibility and generalisability within target dependent sentiment analysis, but before going into the main focus of my work

# Slide 2
I would like to explain what target dependent sentiment analysis is by describing the different levels of sentiment analysis of which the first is document level sentiment analysis. This is the task of given a text like this one predict the sentiment of the text, in this case it is negative.

# Slide 3
Moving to a more fine grained task of aspect based sentiment analysis, this is the task of given a conceptual entity known as an aspect and the text the aspect occurs within predict the sentiment of the text. In this example there are 3 samples as we have 3 aspects that occur within the text.

# Slide 4
Target Dependent Sentiment Analysis also known as TDSA, is the task of given a target and the text that the target occurs within predict the sentiment of the target. This is a similar task to aspect based but the key differences is that the target has to occur within the text which is not the case for aspect based as they are conceptual entities. Now the definition of TDSA has been covered I am going to move on to the main focus of the talk.

# Slide 5
Generalisability within this work is the concept of applying your method across multiple datasets that have different properties. You could state that your method is generalisable if it can perform well across all of these different datasets. Here we have listed what we think are the 5 main different dataset properties. We believe that testing your method for generalisability is important for the real world, as you would like to know what are the weakness and strengths of your new method are which can be found out to some extent by applying your method to different datasets. For instances your method might work well on one type of dataset e.g. Reviews but not on Social media.

# Slide 6
So why have we chosen TDSA as a case study for generalisability. I think this can be shown by this table here. The rows represent different methods and the columns datasets. The ticks represent a method that has been applied to a dataset. The grey out cells occur when the dataset did not exists when the method was created. As you can clearly see there are a lot of unticked cells which shows how little these dataset are utilised. Further more this shows that a lot of the methods have never been fairly compared as they have never been applied to the same dataset. This shows first of all that we don't know truly what is the state of the art in our field as methods are more state of the art on their applied dataset. Second as methods have only been applied to limited datasets and therefore dataset properties we don't know how different methods are affected by different dataset properties. This point can be best shown by the following highlighting.

# Slide 7
The highlighting of the columns represents one dataset property the type property, this furthers my point as we can see clearly here that certain methods ones highlighted in blue have only been applied to one type of dataset the review type therefore not knowing how they might be affected by other dataset types e.g. social media type data.

# Slide 8
Where as there are others shown here in blue again that have never been applied to the review type datasets.

So I hope this table shows why have highlighted the problem in TDSA.

# Slide 9
How can we solve this lack of knowledge? Our answer is to reproduce three complementary methods the ones highlighted in blue that have been applied to varying different datasets, two which have never been applied to review data and the other that has been applied to review but only one social media datasets. Lastly these methods are also different with respect the methods. Vo et al. and Wang et al. are neural pooling methods where Wang et al. extends Vo et al. by incorporating explicit linguistic knowledge through a dependency parser where as Tang is very different by using an LSTM based method.

# Slide 10
Why reproduce?
1. Some methods did not release their code with the paper so reproducing was the only way possible.
2. Reproducing methods that have released their code is still a worth while pursuit as reproducing the method from the paper allows us as a community to find out what is missing in our papers that is vital for reproducing our work.

To motivate this second point the bottom table here represents three different published results of Tang et al.'s method the original, one that re-used the same code based and another that was a reimplementation as you can clearly see none get the same results and they are fairly different accuracy scores but we don't know why. Hence finding a possible reason for this I believe to be a worth while pursuit.

# Slide 11
We now move on to the methods we are reproducing, we are only going to look at the reproducibility results of two method Vo et al. and Tang et al. Vo et al. as mentioned earlier is a Neural Pooling method. it represents all words as word vectors. It splits the sentence up into different contexts. For each context it performs the five pooling methods across all word vectors in that context. Then for each pooled vector for all contexts are concatenated together to create the feature vector that is input into the SVM. This is the general architecture of their method of which they had three main different variants which took into account different contexts and sentiment lexicons.

# Slide 12
The graphs shows on the X axis the different methods of Vo et al. As you can see from the green and orange bars we have successfully reproduced the method which is fantastic from a reproducibility perspective. However we found one interesting finding that applied to this method as well as Wang et al.'s method. If we did not apply scaling to the final feature vector we would not have reproduced their result as shown by this blue column in the graph. Further more scaling was never mentioned in the paper nor in Wang et al's paper however as we clearly show it is of great importance for reproducibility. You could class scaling as a normal best practice post processing technique but I believe anything that has this much of an affect should be mentioned explicitly within the paper and not made an assumption.

# Slide 13
Moving on to Tang et al's method. This was the main architecture of their TD and TC LSTM methods were the TC compared to TD also incorporated the Target word vectors at each time step, they also used as a baseline a standard LSTM which took no target information into account. As shown in the diagram the method is made of Two LSTMs one forward LSTM that was applied over the words that are left of the Target as well as the Target words itself, the second is a backward LSTM applied over the words that are right of the LSTM as well as the Target words. The outputs of the LSTMs are concatenated together and are inputted into a soft max layer.

# Slide 14
First looking at the graph we have the various different method on the X axis and the colours represent different word vectors. Each box plot shows the distribution of scores where the differences between the runs are the initial seed values. As you can see the distribution can vary by quite a lot. This is our second main finding from these reproducibility studies that neural network models for TDSA vary a lot when different seed values are used and can explain the differences that previous work has found when trying to reproduce Tang et al's method. The table on the right shows that if we take the best seed value detonated as Max in the table we can reproduce the method rankings which in this case is TCLSTM is better than TDLSTM which is better than LSTM but this is not the case if we took the mean values.

# Slide 15
Moving on from our reproducibility studies to looking at generalisability. As I stated before we want to see how generalisable these methods are and if any are better or worse on datasets that they have not been applied to before. Here are the datasets we are applying these methods to. As you can see they vary quite a lot with respect to the 5 different dataset properties I showed earlier and this would be the first time methods have been applied to datasets across the different domain, type and medium in TDSA.

# Slide 16
These are the results. A long the X axis are methods and Y axis datasets. The darker the cell the better the score. As there is a lot going on here, I want to highlight only two points to re motivate the reasons why generalisability is important. The first highlighted point is in red, TCLSTM has the highest score for the LSTM methods only on the dataset it was originally applied to the Dong Twitter dataset. All other datasets this method performs worse than its less target aware TDLSTM method and in some case its baseline LSTM method that contains no Target information. This shows that TCLSTM clearly does not generalise well but from a positive aspect it shows that their must be some property in the Dong Twitter dataset that TCLSTM method can exploit to perform that bit better.

# Slide 17
The second point is that certain methods perform really well on certain dataset as shown here. TDParse methods perform very well on the Youtube dataset compared to all other methods. Thus showing again that methods must perform well on certain dataset properties and in this case this could be due to the dataset being the smallest dataset and the method being the only one of the three that incorporated some explicit linguistic knowledge through a dependency parser.

# Slide 18
Thanks for listening, any questions?
