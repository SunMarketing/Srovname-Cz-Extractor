# Srovnáme extractor for Keboola
KBC Docker app for extracting data from Srovnáme (http://srovname.cz)

The Extractor gets list of campaign stats for previous day and saves the data to Storage API. Date of downloaded stats can be changed in configuration.


## Configuration

- **parameters**:
    - **username** - Username to Srovnáme
    - **password** - Password to Srovnáme
    - **bucket** - Name of bucket where the data will be saved
    - **since** *(optional)* - start date of downloaded stats (default is "-1 day")
    - **until** *(optional)* - end date of downloaded stats (default is "-1 day")

- **Example configuration**:
    ```javascript
        {
            "username": "email@example.cs",
            "#password": "secret_password",
            "bucket": "in.c-ex-srovname",
            "since": "-35 day"
        }
    ```

## Output

Data are saved into table **incrementally**:

**stats** - contains marketing stats, columns are:
- **date** 
- **visits**   
- **cpc** 
- **spend**
- **conversion_rates** 
- **orders** 
- **aov**
- **transaction_revenue**
- **pno**


> **NOTICE!**

> - Data can change for last 30 days


## Installation

If you want to run this app standalone:

1. Clone the repository: `git@bitbucket.org:matla/srovname-extractor.git ex-srovname`
2. Go to the directory: `cd ex-srovname`
3. Install composer: `curl -s http://getcomposer.org/installer | php`
4. Install packages: `php composer.phar install`
5. Create folder `data`
6. Create file `data/config.yml` with configuration, e.g.:

    ```
    parameters:
      username:
      password:
      bucket: in.c-srovname
    ```
7. Run: `php src/run.php --data=./data`
8. Data tables will be saved to directory `data/out/tables`
