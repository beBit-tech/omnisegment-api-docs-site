# API Error Handbook

* Response status code
    * `502 Bad Gateway` `503 Service Unavailable` `504 Gateway timeout`

       If you receive one of the above status codes, retry again every **five minutes** until getting other status code or having retried over **five times**.
