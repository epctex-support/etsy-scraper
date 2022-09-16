# Actor - Etsy Scraper

## Etsy scraper

Since Etsy doesn't provide an API, this actor should help you to retrieve data from it.

The Etsy data scraper supports the following features:

-   Scrape product details - You can scrape attributes like images, seller information, photos, time of listing and many more. You can find details below.

-   Scrape search results - You can scrape for a specific search result by keyword.

-   Scrape and filter any categories - You can provide any category with any kind of filter that you want.

-   Define maximum number of pages that needs to be scraped - If you only want to scrape first 3 pages, there is an option for that.

#### Etsy specific

Don't worry when you get little bit different products than you saw in browser page. Etsy is ordering products differently for each user.

## Bugs, fixes, updates and changelog

This scraper is under active development. If you have any feature requests you can create an issue from [here](https://github.com/epctex/etsy-scraper/issues).

### Incoming Changes

-   Fetching product reviews
-   Fetch seller profile

## Setup & Usage

You can see how this actor works in this video:

### Start URLs

[![Apify - Etsy Scraper - Using Start URLs](https://img.youtube.com/vi/LsnuDePh-0A/0.jpg)](https://www.youtube.com/watch?v=LsnuDePh-0A)

You can check the output of this video [here](https://api.apify.com/v2/datasets/OKZ3MItTB1CXqmabi/items?clean=true&format=json).

### Using Search

[![Apify - Etsy Scraper - Using Search ](https://img.youtube.com/vi/BdJDDQSFJnQ/0.jpg)](https://www.youtube.com/watch?v=BdJDDQSFJnQ)

You can check the output of this video [here](https://api.apify.com/v2/datasets/IcDQQr47WDtbAivoy/items?clean=true&format=json).

## Input Parameters

The input of this scraper should be JSON containing the list of pages on Etsy that should be visited. Required fields are:

| Field                | Type    | Description                                                                                                        |
| -------------------- | ------- | ------------------------------------------------------------------------------------------------------------------ |
| startUrls            | Array   | (optional) List of Etsy URLs. You should only provide category detail, product detail, seller items or search URLs |
| includeDescription   | Boolean | (optional) If you want to fetch description HTML (or text) you can enable this option. Default value is `false`.   |
| maxItems             | Integer | (optional) You can limit scraped products. This should be useful when you search through the big subcategories.    |
| endPage              | Integer | (optional) Final number of page that you want to scrape. Default is `Infinite`.                                    |
| search               | String  | (optional) Keyword that can be searched in Etsy search engine.                                                     |
| extendOutputFunction | String  | (optional) Function that takes a JQuery handle ($) as argument and returns object with data                        |
| proxy                | Object  | Proxy configuration                                                                                                |

This solution requires the use of **Proxy servers**, either your own proxy servers or you can use <a href="https://www.apify.com/docs/proxy">Apify Proxy</a>.

##### Tip

When you want to have a filtering over a category URL; go to Etsy, create filters over the category and copy and paste the link as one of the **startUrl**.

If you would like to scrape only the first page of a search list or category list, then put the link for the page and have the `endPage` as 1.

With the last approach that explained above you can also fetch any interval of pages. If you provide the 5th page of a category and define the `endPage` parameter as 6 then you'll have the 5th and 6th pages only.

### Compute Unit Consumption

The actor optimized to run blazing fast and scrape many as product as possible. Therefore, it forefronts all product detail requests. If actor doesn't block very often it'll scrape 50 products in 1 minute with ~0.04-0.05 compute units.

### Etsy Scraper Input example

```json
{
    "startUrls": [
        "https://www.etsy.com/c/clothing-and-shoes?ref=pagination&page=4"
    ],
    "search": "apple watch",
    "endPage": 6,
    "includeDescription": true,
    "maxItems": 100
}
```

## During the Run

During the run, the actor will output messages letting you know what is going on. Each message always contains a short label specifying which page from the provided list is currently specified.
When items are loaded from the page, you should see a message about this event with a loaded item count and total item count for each page.

If you provide incorrect input to the actor, it will immediately stop with failure state and output an explanation of what is wrong.

## Etsy Export

During the run, the actor stores results into a dataset. Each item is a separate item in the dataset.

You can manage the results in any languague (Python, PHP, Node JS/NPM). See the FAQ or <a href="https://www.apify.com/docs/api" target="blank">our API reference</a> to learn more about getting results from this Etsy actor.

## Scraped Etsy Products

The structure of each item in Etsy products looks like this:

```json
{
	"url": "https://www.etsy.com/listing/498417899/edc-slim-valet-personalized-pocket?ga_order=most_relevant&ga_search_type=all&ga_view_type=gallery&ga_search_query=&ref=sr_gallery-4-29&frs=1&cns=1&col=1",
	"name": "EDC Slim Valet - Personalized Pocket Organizer, Handmade in the USA\nRegions Etsy does business in:",
	"images": [
		"https://i.etsystatic.com/13963159/r/il/3d1876/3180744258/il_794xN.3180744258_olzc.jpg",
		"https://i.etsystatic.com/13963159/r/il/a3c7cf/1617748881/il_794xN.1617748881_1o26.jpg",
		"https://i.etsystatic.com/13963159/r/il/9eb645/1570294448/il_794xN.1570294448_oe8w.jpg",
		"https://i.etsystatic.com/13963159/r/il/6b2a6a/1570293332/il_794xN.1570293332_8z6i.jpg",
		"https://i.etsystatic.com/13963159/r/il/39f7ad/3180744724/il_794xN.3180744724_2baa.jpg",
		"https://i.etsystatic.com/13963159/r/il/08b20b/3180745230/il_794xN.3180745230_95a2.jpg",
		"https://i.etsystatic.com/13963159/r/il/31e60f/3494515703/il_794xN.3494515703_54ci.jpg",
		"https://i.etsystatic.com/13963159/r/il/352b64/3458390857/il_794xN.3458390857_4ity.jpg"
	],
	"seller": {
		"name": "RutsuDesigns",
		"url": "https://www.etsy.com/shop/RutsuDesigns?ref=simple-shop-header-name&listing_id=498417899",
		"sales": 483,
		"rating": 4.9375,
		"numberOfReviews": 47
	},
	"Price": "$49.00+",
	"variations": [
		{
			"label": "Color",
			"values": [
				"Dark Chocolate",
				"Mahogany",
				"Cordovan"
			]
		},
		{
			"label": "Personalize / Monogram",
			"values": [
				"None ($49.00)",
				"Monogram ($59.00)"
			]
		}
	],
	"highlights": [
		"Handmade",
		"Materials: leather, metal rivets"
	],
	"listedOn": "Jul 12, 2022",
	"favorites": 772
}
```
