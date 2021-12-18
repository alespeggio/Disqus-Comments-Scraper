# Disqus Comments Scraper

## Overview

![Disqus Logo](https://c.disquscdn.com/next/c393ff4/marketing/assets/img/brand/disqus-logo-white-blue.png)

This repository provides a very basic scraper that can be used in order to extract comments from any website that does have Disqus comments embedded. 

## Installation 

Assuming that Python is installed, all the required packages can be installed with `pip install -r requirements.txt`

## Running the scraper

The scraper can be used in order to scrape comments from Disqus and store them as a formatted json file. The scraper, which uses Selenium to load and scrape comment, can be launched simply with the command `python3 main.py`. 

However, several additional arguments can be passed in order to customize the scraper behaviour: 

* `url_to_scrape`: If you want to scrape only from a single web page simply pass the url of that web page
* `all_urls_path`: The file path to the local txt file with a list of all the urls we want to scrape from. The scraper assumes the files has one url per line with no separator or special characters. Notice that `url_to_scrape` and `all_urls_path` are mutually esclusive. Hence, only one of the two can be passed as argument. 
* `headless`: Whether the execution should be headless or not (if not headless you will see the scraper interacting with the actual chrome page). By default this is set to `False`
* `scraper_delay`: To scrape comments from Disqus the comments first need to be loaded. Therefore a small delay (in seconds) is required. The value can be passed as a number and by default `scraper_delay` is set to `1`.
* `disqus_wrapper_tag`: Disqus comments are inside an `iframe` loaded inside the page. This iframe is usually wrapped by a custom html tag defined by the webpage developer. As to load comments we need to scroll to that specific section we need to know where the comments are. Hence, for this argument you need to specify the html tag of that wrapper element (i.e. `<div>`). 
* `disqus_wrapper_attribute`: As we need to identify which `disqus_wrapper_tag` to select, you also need to specify the attribute you want to use to uniquely identify this tag (i.e. class or id)
* `disqus_wrapper_attribute_value`: The specific value of the attribute for the tag we want to select (i.e. unique_div_id)
* `popup_tag`: Sometimes the webpage has a popup that needs to be closed. If the popup is not closed then comments can't be loaded correctly. For this reason, with this parameter we can specify the tag of the element that has to be clicked to close the popup (i.e. <div>) 
* `popup_attribute`: The attribute of the popup element we want to select (i.e. class)
* `popup_attribute_value`: The value of the attribute for the popup we want to close (i.e. close_popup_button)


An example of the command that can be issued is shown below

```bash
python main.py --all_urls_path=file.txt 
--headless=False 
--scraper_delay=5 
--popup_tag=button 
--popup_attribute=class 
--popup_attribute_value="close-btn-handler close-btn-ui banner-close-button" 
--disqus_wrapper_tag=div 
--disqus_wrapper_attribute=id 
--disqus_wrapper_attribute_value=disqus-block_1-0
```

### Result

The scraped comments are saved in `data/output.json`. Notice that multiple runs of the scraper will append results to the file. Hence, to start with a new empty file delete `output.json` from the folder. 

Laslty, the json file contains a line for each page scraped. The json for each line has the following structure

```json 
{
	"author": "",
   "published_date": "",
   "published_date_timestamp": "",
   "comment": "",
   "likes": "",
   "dislikes": "",
   "replies": []           
}
```

Notice that key replies is a list of Json objects whith exaclty the same structure which are in reply to the specific comment. Therefore, replies do have a nested and tree-like structure. 



                    
                    
   