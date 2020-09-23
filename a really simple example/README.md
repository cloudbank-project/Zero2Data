# Really Simple Example

Let's just build a data service that has no data source as such. You send it a number and it returns a prime factorization. The code will sit in a serverless Lambda function.


```
# From Zero2Data / Simple data service on AWS
# In browser using the provided endpoint: https://kep5pu8n09.execute-api.us-west-2.amazonaws.com/default/primefactors?n=4700

import json

def lambda_handler(event, context):
    return_msg, n0 = '', int(event["queryStringParameters"]['n'])

    if n0 < 2:
        n0 = 103598728
        return_msg += 'Could not parse input; using n = '

    return_msg += str(n0) + ' = '
    prime_factors, factor_candidate, n = [], 2, n0
    while factor_candidate ** 2 <= n:
        if n % factor_candidate:
            if factor_candidate == 2: factor_candidate = 3
            else:                     factor_candidate += 2
        else:
            n = n / factor_candidate
            prime_factors.append(factor_candidate)
    if n > 1: prime_factors.append(n)
        
    npf = len(prime_factors)
    for i in range(npf - 1): return_msg += str(prime_factors[i]) + ' * '
    return_msg += str(int(prime_factors[npf - 1]))
    return { "statusCode": 200, "body": return_msg }
```
