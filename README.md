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

## Need to find product pairs between Etsy and another online shop?

Use the [AI Product Matcher](https://apify.com/equidem/ai-product-matcher?fpr=yhdrb)🔗. This AI model allows you to compare items from different web stores, identifying exact matches and comparing real-time data obtained via web scraping. 

With the AI Product Matcher, you can use scraped product data to monitor product matches across the industry, implement dynamic pricing for your website, replace or complement manual mapping, and obtain realistic estimates against your competition for upcoming promo campaigns. Most importantly, it is relatively easy to get started with (just follow [this guide](https://blog.apify.com/product-matching-ai-pricing-intelligence-web-scraping/)) and is able to **match thousands of product pairs**.

## Bugs, fixes, updates and changelog

This scraper is under active development. If you have any feature requests you can create an issue from [here](https://github.com/epctex/etsy-scraper/issues).

### Incoming Changes

-   Fetching product reviews
-   Fetch seller profile

## Input Parameters

The input of this scraper should be JSON containing the list of pages on Etsy that should be visited. Possible fields are:

- `search`: (Optional) (String) Keyword that can be searched in Etsy search engine.

- `startUrls`: (Optional) (Array) List of Etsy URLs. You should only provide category detail, product detail, seller items or search URLs.

- `includeDescription`: (Optional) (Boolean) If you want to fetch description HTML (or text) you can enable this option. Default value is `false`.

- `endPage`: (Optional) (Number) Final number of page that you want to scrape. Default is `Infinite`. This is applies to all `search` request and `startUrls` individually.

- `maxItems`: (Optional) (Number) You can limit scraped items. This should be useful when you search through the big lists or search results.

- `proxy`: (Required) (Proxy Object) Proxy configuration.

- `extendOutputFunction`: (Optional) (String) Function that takes a JQuery handle ($) as argument and returns object with data.

- `customMapFunction`: (Optional) (String) Function that takes each objects handle as argument and returns object with executing the function.

This solution requires the use of **Proxy servers**, either your own proxy servers or you can use <a href="https://www.apify.com/docs/proxy">Apify Proxy</a>.

### Tip

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
		"sales": 538,
		"rating": 4.9583,
		"numberOfReviews": 48
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
	"listedOn": "Dec 26, 2022",
	"favorites": 806,
	"relatedSearches": [
		{
			"name": "EDC Pocket Organizer",
			"link": "https://www.etsy.com/market/edc_pocket_organizer?ref=seller_tag_bottom_image-0"
		},
		{
			"name": "EDC Wallet",
			"link": "https://www.etsy.com/market/edc_wallet?ref=seller_tag_bottom_image-1"
		},
		{
			"name": "EDC Organizer",
			"link": "https://www.etsy.com/market/edc_organizer?ref=seller_tag_bottom_image-2"
		},
		{
			"name": "EDC Pocket",
			"link": "https://www.etsy.com/market/edc_pocket?ref=seller_tag_bottom_image-3"
		},
		{
			"name": "Everyday Carry Gear",
			"link": "https://www.etsy.com/market/everyday_carry_gear?ref=seller_tag_bottom_image-4"
		},
		{
			"name": "Pocket Organizer",
			"link": "https://www.etsy.com/market/pocket_organizer?ref=seller_tag_bottom_image-5"
		},
		{
			"name": "Leather Organizer",
			"link": "https://www.etsy.com/market/leather_organizer?ref=seller_tag_bottom_image-6"
		},
		{
			"name": "EDC",
			"link": "https://www.etsy.com/market/edc?ref=seller_tag_bottom_image-7"
		},
		{
			"name": "EDC Gear",
			"link": "https://www.etsy.com/market/edc_gear?ref=seller_tag_bottom_image-8"
		},
		{
			"name": "Minimalist EDC",
			"link": "https://www.etsy.com/market/minimalist_edc?ref=seller_tag_bottom_image-9"
		},
		{
			"name": "Gift for Men",
			"link": "https://www.etsy.com/market/gift_for_men?ref=seller_tag_bottom_image-10"
		},
		{
			"name": "Holiday Gift",
			"link": "https://www.etsy.com/market/holiday_gift?ref=seller_tag_bottom_image-11"
		},
		{
			"name": "Rutsu Designs",
			"link": "https://www.etsy.com/market/rutsu_designs?ref=seller_tag_bottom_text-0"
		}
	]
}
```

## Contact
Please visit us through [epctex.com](https://epctex.com) to see all the products that is available for you. If you are looking for any custom integration or so, please reach out to us through the chat box in [epctex.com](https://epctex.com). In need of support? [devops@epctex.com](mailto:devops@epctex.com) is at your service.
