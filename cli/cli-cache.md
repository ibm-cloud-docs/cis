---

copyright:
  years: 2018
lastupdated: "2018-05-21"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Cache

The following `cache` commands are available:

* Purge cache
* Show cache settings
* Update cache settings

## Purge Cache
### NAME
  `cache-purge` -  Clear cached assets file by file or entirely for a given DNS domain to guarantee served assets are updated.

### USAGE
  `ibmcloud cis cache-purge DNS_DOMAIN_ID (--all | -f, --file file1,file2,...) [-i, --instance INSTANCE_NAME]`

### OPTIONS

   * `-i, --instance INSTANCE_NAME` (Optional) Instance name. If not set, the context instance specified by `ibmcloud cis instance-set` is used.

   *  `--all` Clear cached assets entirely, when this option exists, users are asked to confirm `Y/N`. Purging all cached files increases page load times while the files are being re-created. This process removes all of your cached data on all edge servers.

   * `-f, --file** file1,file2,...`  an array of files (separated by commas) that should be cleared from cache. You may purge up to 30 files at a time with comma-separated files. To specify a file, you must enter the full path. Wildcards are not supported at this time.


#### Output messages:
Result of cache purging.


## Show cache settings

### NAME
  `cache-settings` - Get caching settings for a given DNS domain.

### USAGE
  `ibmcloud cis cache-settings DNS_DOMAIN_ID [-i, --instance INSTANCE_NAME]`

### OPTIONS

   * `-i, --instance INSTANCE_NAME`  (Optional) Instance name. If not set, the context instance specified by `ibmcloud cis instance-set` is used.

#### Output messages:

  * Caching Level
  * Browser Expiration
  * Development Mode

## Update cache settings

### NAME
  `cache-settings-update` - Update cache settings for a give DNS domain.

### USAGE
  `ibmcloud cis cache-settings-update DNS_DOMAIN_ID [--caching-level LEVEL][--browser-expiration EXPIRATION][--development-mode (enabled | disabled)][-i, --instance INSTANCE_NAME]`

### OPTIONS

   * `-i, --instance INSTANCE_NAME`  (Optional) Instance name. If not set, the context instance specified by `ibmcloud cis instance-set` is used.
   

   * `--caching-level _value_`  Specify under what URL conditions you want to deliver cached assets to the user.  Valid _value_ tokens are: `no-query-string`,  `query-string-independent`,  `query-string-dependent`.
   
     * `no-query-string` Only delivers resources from cache when there is no query string.                    
     * `query-string-independent` Delivers the same resource to everyone independent of the query string.
     * `query-string-dependent` Delivers a different resource each time the query string changes.


   * `--browser-expiration _value_` Specify how long you want the user's browser to store cached assets.                Valid _value_ tokens are: `respect-existing-header`, `30M`, `1h`, `2h`, `4h`, `8h`, `16h`, `1d`, `3d`, `8d`, `16d`, `1m`, `6m`, `1y`.                         
     * `30M` means `30 minutes`
     * `1h` means `1 hour`
     * `1d` means `1 day`
     * `1m` means `1 month`
     * `1y` means `1 year`


   * `--development-mode _value_` Bypass all edge caches and send traffic toward your origin servers.


#### Output messages:
The output message contains the result of your cache settings update.
