---
layout: default
title: (Deprecated)  Perceptron and Winnow
theme:
    name: retro-mahout
---
# Introduction to Item-Based Recommendations with Hadoop

##Overview

Mahout’s item based recommender is a flexible and easily implemented algorithm with a diverse range of applications. The minimalism of the primary input file’s structure and availability of ancillary filtering controls can make sourcing required data and shaping a desired output both efficient and straightforward.

Typical use cases include:

* Recommend products to customers via an eCommerce platform (think: Amazon, Netflix, Overstock)
* Identify organic sales opportunities
* Segment users/customers based on similar item preferences

Broadly speaking, Mahout's item-based recommendation algorithm takes as input customer preferences by item and generates an output recommending similar items with a score indicating whether a customer will "like" the recommended item.

One of the strengths of the item based recommender is its adaptability to your business conditions or research interests. For example, there are many available approaches for providing product preference. One such method is to calculate the total orders for a given product for each customer (i.e. Acme Corp has ordered Widget-A 5,678 times) while others rely on user preference captured via the web (i.e. Jane Doe rated a movie as five stars, or gave a product two thumbs’ up).

Additionally, a variety of methodologies can be implemented to narrow the focus of Mahout's recommendations, such as:

* Exclude low volume or low profitability products from consideration
* Group customers by segment or market rather than using user/customer level data
* Exclude zero-dollar transactions, returns or other order types
* Map product substitutions into the Mahout input (i.e. if WidgetA is a recommended item replace it with WidgetX)

The item based recommender output can be easily consumed by downstream applications (i.e. websites, ERP systems or salesforce automation tools) and is configurable so users can determine the number of item recommendations generated by the algorithm.

##Example

Testing the item based recommender can be a simple and potentially quite rewarding endeavor. Whereas the typical sample use case for collaborative filtering focuses on utilization of, and integration with, eCommerce platforms we can instead look at a potential use case applicable to most businesses (even those without a web presence). Let’s look at how a company might use Mahout’s item based recommender to identify new sales opportunities for an existing customer base. First, you’ll need to get Mahout up and running, the instructions for which can be found [here](https://mahout.apache.org/users/basics/quickstart.html). After you've ensured Mahout is properly installed, we’re ready to run a quick example.

**Step 1: Gather some test data**

Mahout’s item based recommender relies on three key pieces of data: *userID*, *itemID* and *preference*. The “users” could be website visitors or simply customers that purchase products from your business. Similarly, items could be products, product groups or even pages on your website – really anything you would want to recommend to a group of users or customers. For our example let’s use customer orders as a proxy for preference. A simple count of distinct orders by customer, by product will work for this example. You’ll find as you explore ways to manipulate the item based recommender the preference value can be many things (page clicks, explicit ratings, order counts, etc.). Once your test data is gathered put it in a *.txt* file separated by commas with no column headers included.

**Step 2: Pick a similarity measure**

Choosing a similarity measure for use in a production environment is something that requires careful testing, evaluation and research. For our example purposes, we’ll just go with a Mahout similarity classname called *SIMILARITY_LOGLIKELIHOOD*.

**Step 3: Configure the Mahout command**

Assuming your *JAVA_HOME* is appropriately set and Mahout was installed properly we’re ready to configure our syntax. Enter the following command:

    $ mahout recommenditembased -s SIMILARITY_LOGLIKELIHOOD -i /path/to/input/file -o /path/to/desired/output --numRecommendations 25

Running the command will execute a series of jobs the final product of which will be an output file deposited to the directory specified in the command syntax. The output file will contain two columns: the *userID* and an array of *itemIDs* and scores.

**Step 4: Making use of the output and doing more with Mahout**

The output file generated in our simple example can be transformed using your tool of choice and consumed by downstream applications. There exist a variety of configuration options for Mahout’s item based recommender to accommodate custom business requirements; exploring and testing various configurations to suit your needs will doubtless lead to additional questions. Our user community is accessible via our [mailing list](https://mahout.apache.org/general/mailing-lists,-irc-and-archives.html) and the book *Mahout In Action* is a fantastic (but slightly outdated) starting point. 