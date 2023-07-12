[https://apify.com/epctex/advanced-glassdoor-scraper](https://apify.com/epctex/advanced-glassdoor-scraper?fpr=yhdrb)

# Actor - Glassdoor Scraper

## Glassdoor scraper

Since Glassdoor doesn't provide a good and free API, this actor should help you to retrieve data from it.

The Glassdoor data scraper supports the following features:

-   Search any keyword - You can search any keyword you would like to have and get the results. No limits!

-   Get extensive company information - Get all information about a company right away!

-   Looking for jobs? You are at the right place! - Retrieve all the job information of a company supported by filters. Extremely fast data retrieval!

-   All detailed salary information is at your fingertips! - Salary information and all the detailed pricing is at your service!

-   Company reviews! - All the extended reviews, company information, ratings, and many other stuff!

-   Interviews - Retrieve all the interviews of a company. Super simple, easy usage!


## Bugs, fixes, updates, and changelog

This scraper is under active development. If you have any feature requests you can create an issue from [here](https://github.com/epctex/glassdoor-scraper/issues).


## Input Parameters

The input of this scraper should be JSON containing the list of pages on Glassdoor that should be visited. Required fields are:

- `search`: (Optional) (String) Keyword that you want to search on Glassdoor.

- `startUrls`: (Optional) (Array) List of Glassdoor URLs. It should be a company, salary, interview, job, search, or any listing URL.

- `endPage`: (Optional) (Number) Final number of page that you want to scrape. The default is `Infinite`. This applies to all `search` requests and `startUrls` individually.

- `maxItems`: (Optional) (Number) You can limit scraped items. This should be useful when you search through the big lists or search results.

- `proxy`: (Required) (Proxy Object) Proxy configuration.

- `extendOutputFunction`: (Optional) (String) Function that takes a JQuery handle ($) as an argument and returns an object with data.

- `customMapFunction`: (Optional) (String) Function that takes each object's handle as an argument and returns the object with executing the function.

This solution requires the use of **Proxy servers**, either your own proxy servers or you can use [Apify Proxy](https://www.apify.com/docs/proxy).

### Tip

When you want to scrape over a specific list URL, just copy and paste the link as one of the **startUrl**.

If you would like to scrape only the first page of a list then put the link for the page and have the `endPage` as 1.

With the last approach that is explained above you can also fetch any interval of pages. If you provide the 5th page of a list and define the `endPage` parameter as 6 then you'll have the 5th and 6th pages only.

### Compute Unit Consumption

The actor is optimized to run blazing fast and scrape as many items as possible. Therefore, it forefronts all the detailed requests. If the actor doesn't block very often it'll scrape 100 listings in 2 minutes with ~0.25-0.45 compute units.

### Glassdoor Scraper Input example

```json
{
  "startUrls":[
    "https://www.glassdoor.com/Overview/Working-at-Elastic-EI_IE751551.11,18.htm",
    "https://www.glassdoor.com/Reviews/Elastic-Reviews-E751551.htm",
    "https://www.glassdoor.com/Reviews/Elastic-Reviews-E751551.htm?filter.iso3Language=eng&filter.employmentStatus=REGULAR&filter.employmentStatus=PART_TIME&filter.searchCategory=CULTURE",
    "https://www.glassdoor.com/Interview/Elastic-Interview-Questions-E751551.htm",
    "https://www.glassdoor.com/Interview/Elastic-Marketing-Assistant-Interview-Questions-EI_IE751551.0,7_KO8,27.htm#InterviewReview_76289952",
    "https://www.glassdoor.com/Job/elastic-jobs-SRCH_KO0,7.htm",
    "https://www.glassdoor.com/job-listing/federal-account-executive-nga-elastic-JV_IC1138213_KO0,29_KE30,37.htm?jl=1008611278488&pos=107&ao=1136043&s=58&guid=000001884d59c10aafb263d8cfe0037f&src=GD_JOB_AD&t=SR&vt=w&ea=1&cs=1_cd6d3492&cb=1684924907959&jobListingId=1008611278488&jrtk=3-0-1h16ljg9dk6fr801-1h16ljg9ti9j2800-c74621bdf8ed430d-&ctt=1684925008345",
    "https://www.glassdoor.com/Salary/Elastic-Software-Engineer-Salaries-E751551_D_KO8,25.htm"
  ],
  "maxItems": 100,
  "endPage": 5,
  "proxy":{
    "useApifyProxy":true
  }
}

```

## During the Run

During the run, the actor will output messages letting you know what is going on. Each message always contains a short label specifying which page from the provided list is currently specified.
When items are loaded from the page, you should see a message about this event with a loaded item count and total item count for each page.

If you provide incorrect input to the actor, it will immediately stop with a failure state and output an explanation of what is wrong.

## Glassdoor Export

During the run, the actor stores results into a dataset. Each item is a separate item in the dataset.

You can manage the results in any language (Python, PHP, Node JS/NPM). See the FAQ or <a href="https://www.apify.com/docs/api" target="blank">our API reference</a> to learn more about getting results from this Glassdoor actor.

## Scraped Glassdoor Properties

The structure of each item in Glassdoor looks like this:

### Job Detail

```json
{
    "type": "job",
    "url": "https://www.glassdoor.com/job-listing/federal-account-executive-nga-elastic-JV_IC1138213_KO0,29_KE30,37.htm?jl=1008611278488&pos=107&ao=1136043&s=58&guid=000001884d59c10aafb263d8cfe0037f&src=GD_JOB_AD&t=SR&vt=w&ea=1&cs=1_cd6d3492&cb=1684924907959&jobListingId=1008611278488&jrtk=3-0-1h16ljg9dk6fr801-1h16ljg9ti9j2800-c74621bdf8ed430d-&ctt=1684925008345",
    "title": "Federal Account Executive - NGA",
    "body": "Elastic is a free and open search company that powers enterprise search, observability, and security solutions built on one technology stack that can be deployed anywhere. ",
    "bodyHTML": "<div><div><p>Elastic is a free and open search company that powers enterprise search, observability, and security solutions built on one technology stack that can be deployed anywhere.</p></div></div>",
    "jobLocation": {
        "country": "United States",
        "cityName": "Washington, DC",
        "stateName": "District of Columbia"
    },
    "company": {
        "name": "Elastic",
        "location": "Mountain View, CA",
        "size": "1001 to 5000 Employees",
        "type": "Company - Public",
        "sector": "Information Technology",
        "founded": 2012,
        "industry": "Enterprise Software & Network Solutions",
        "revenue": "$100 to $500 million (USD)",
        "ratings": [
            {
                "title": "Overall",
                "rating": 3.7
            },
            {
                "title": "CEO",
                "rating": 0.65
            },
            {
                "title": "CEO Ratings Count",
                "rating": 151
            },
            {
                "title": "Recommend",
                "rating": 0.65
            },
            {
                "title": "Career Opportunities",
                "rating": 3.4
            },
            {
                "title": "Compensation & Benefits",
                "rating": 4.2
            },
            {
                "title": "Culture & Values",
                "rating": 3.8
            },
            {
                "title": "Senior Management",
                "rating": 3.2
            },
            {
                "title": "Work/Life Balance",
                "rating": 4.1
            }
        ]
    }
}
```

### Review Detail

```json
{
    "type": "review",
    "url": "https://www.glassdoor.com/Reviews/Employee-Review-Elastic-RVW76656731.htm",
    "title": "Company",
    "isCurrentEmployee": true,
    "date": "2023-05-22T05:45:39.153",
    "isAnonymousEmployee": false,
    "ratings": [
        {
            "title": "Work/Life Balance",
            "rating": 4
        },
        {
            "title": "Overall",
            "rating": 5
        },
        {
            "title": "Culture & Values",
            "rating": 4
        },
        {
            "title": "Diversity & Inclusion",
            "rating": 4
        },
        {
            "title": "Senior Management",
            "rating": 5
        },
        {
            "title": "Career Opportunities",
            "rating": 4
        },
        {
            "title": "Compensation and Benefits",
            "rating": 5
        }
    ],
    "pros": "Excellent leadership, product, and company vision.",
    "cons": "We have been through many leadership transitions but are on the other side.",
    "reviews": [
        {
            "title": "Recommend",
            "isOK": true
        },
        {
            "title": "CEO Approval",
            "isOK": true
        },
        {
            "title": "Business Outlook",
            "isOK": true
        }
    ]
}
```

### Salary Detail

```json
{
    "type": "salary",
    "title": "Senior Software Engineer",
    "location": "Los Angeles, CA",
    "totalPay": {
        "lower": 172000,
        "upper": null
    },
    "base": 172000,
    "additional": 0,
    "stock": null,
    "yearsOfExperience": "15+ years",
    "submittedDate": "Dec 4, 2022"
}
```

### Company Detail

```json
{
    "type": "company",
    "url": "https://www.glassdoor.com/Overview/Working-at-Elastic-EI_IE751551.11,18.htm",
    "website": "www.elastic.co",
    "logo": "https://media.glassdoor.com/sql/751551/elastic-squarelogo-1559879227505.png",
    "name": "Elastic",
    "size": "1001 to 5000 Employees",
    "companyType": "Company - Public",
    "revenue": "$100 to $500 million (USD)",
    "stock": "ESTC",
    "headquarters": "Mountain View, CA",
    "founded": 2012,
    "industry": "Enterprise Software & Network Solutions",
    "competitors": [],
    "description": "At Elastic, we see endless possibility in a world of endless data. And we use the power of search to help people and organizations turn that possibility into results. \n\nElastic is the leading platform for search-powered solutions. We help organizations, their employees, and their customers accelerate the results that matter. With solutions in Enterprise Search, Observability, and Security, we help enhance customer and employee search experiences, keep mission-critical applications running smoothly, and protect against cyber threats.\n\nDelivered wherever data lives, in one cloud, across many clouds, or on-prem, Elastic enables organizations worldwide to use the power of Elastic, including Netflix, Uber, BBC, Microsoft, and thousands of others.\n\nElastic was built on a foundation of being free and open, which trickles down to how we work. We’re a distributed organization and have been from the beginning. Being distributed isn’t just a way of doing business—it’s a mindset that is at the core of our culture. \n\nElastic is publicly traded on the NYSE under the symbol ESTC. Learn more at elastic.co.",
    "mission": "We help people around the world do great things with their data. Our products are extending what's possible with data, and deliver on the promise that good things come from connecting the dots.",
    "awards": [
        {
            "name": "100 Large Best Places to Work New York City",
            "year": 2023,
            "awardedBy": "Builtin"
        }
    ]
}
```

### Interview Detail

```json
{
    "type": "interview",
    "url": "https://www.glassdoor.com/Interview/Elastic-Marketing-Assistant-Interview-Questions-EI_IE751551.0,7_KO8,27.htm#InterviewReview_76289952",
    "reviewDate": "2023-05-10T13:12:11.153",
    "id": 76289952,
    "title": "Marketing Assistant",
    "source": null,
    "location": "Switzerland",
    "interviewDate": null,
    "process": "The interview process is very organised and everyone involved is very positive and supportive. In case you do not get the position you applied for, they give very detailed feedback.",
    "questions": [
        "Tell us about your background and why you would be a good fit for this role?"
    ],
    "reviews": [
        {
            "title": "Offer",
            "result": "NO_OFFER"
        },
        {
            "title": "Experience",
            "result": "POSITIVE"
        },
        {
            "title": "Interview",
            "result": "AVERAGE"
        }
    ]
}
```

## Contact
Please visit us through [epctex.com](https://epctex.com) to see all the products that are available for you. If you are looking for any custom integration or so, please reach out to us through the chat box in [epctex.com](https://epctex.com). In need of support? [devops@epctex.com](mailto:devops@epctex.com) is at your service.
