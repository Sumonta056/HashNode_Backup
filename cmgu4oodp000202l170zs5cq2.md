---
title: "Weird JS - 2 (Falsy Values): Why Not to Use “!”, “==” and “===”?"
seoTitle: "Understanding Falsy Values in JavaScript"
seoDescription: "Explore the quirks of JavaScript falsy values, type coercion, and equality operators to avoid common coding mishaps and unexpected bugs"
datePublished: Fri Oct 17 2025 00:46:22 GMT+0000 (Coordinated Universal Time)
cuid: cmgu4oodp000202l170zs5cq2
slug: weird-js-2-falsy-values-why-not-to-use-and
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1760661555160/eb7917c3-9d36-42ca-b683-a8ff6620d528.png
tags: software-development, javascript, web-development, software-engineering, frontend-development

---

Hey there, curious minds! 👋

Welcome to my newsletter, where I share what I’ve been learning, thinking about, and exploring in the tech world. If you don’t know me:

Hi, I am [Sumonta Saha Mri](https://github.com/Sumonta056)[dul.](https://github.com/Sumonta056) I’m an Associate **Software Engineer** at Cefalo. I regularly share what I learn through weekly posts on [**Linke**](https://www.linkedin.com/in/sumonta-saha-mridul-b35bb61a0/)[**dIn**, **Dev**](https://www.linkedin.com/in/sumonta-saha-mridul-b35bb61a0/)**. to**, and **Medium**. Also, I run a small [**YouTube ch**](https://www.youtube.com/@LearnCodewithPS5638)[**annel**](https://github.com/Sumonta056) where I try to share helpful content for developers.

JavaScript is one of those languages that looks simple at first glance, but hides some tricky **surprises. One** of the most common sources of confusion comes from how it handles **falsy values**, **type coercion**, and the difference between == and ===.

While doing and getting code reviews at [**Cefalo Bangladesh Ltd.**](https://www.linkedin.com/showcase/cefalobangladesh/) I often came across feedback from the weird JS concepts that we normally look perfect, but in some corner cases, it shows a completely different face, which leads to breaking the code or the system. That made me dig deeper into their use cases, understand the key differences, and learn when to use which, because choosing the wrong one can lead to unexpected bugs or behavior.

### **Why JavaScript is Weird?**

Let’s see this example, try to find what's going wrong here!

![Article content](https://media.licdn.com/dms/image/v2/D5612AQGlxnr7Q6Jw8w/article-inline_image-shrink_1500_2232/B56ZnW7nUkI8AU-/0/1760247578420?e=1763596800&v=beta&t=Gaa6JSIpJCHt3OyaoprDjw46CfOh2A2Gbwx4VHHGnko align="left")

Did you spot the breaking issue?

At first, this looks fine. You’re checking **if** favoriteNumber **exists**, and only then returning the object. But here’s the catch for this example

![Article content](https://media.licdn.com/dms/image/v2/D5612AQHoODUgpLSRoQ/article-inline_image-shrink_1500_2232/B56ZnW8OkjIYAU-/0/1760247737476?e=1763596800&v=beta&t=GeD7AtWtSyaLoSUgRaTfb8sS-4cKG9jgwaDQtt2IJ5w align="left")

The break point !

Why? Because 0 is a **falsy value** in JavaScript. That means !0 becomes true, even though 0 might be a perfectly valid input.

If you check if (!favoriteNumber) to detect “missing” values, you will also treat other *falsy* values as missing

* !undefined → true
    
* !null → true
    
* !0 → true ← **this is the gotcha** (so 0 looks like “missing”)
    
* !"" → true
    
* !NaN → true
    

> **That's why they call JavaScript : Mr Weird JS**

![Article content](https://media.licdn.com/dms/image/v2/D5612AQFNGDWB79qreA/article-inline_image-shrink_1000_1488/B56ZnYJBNxJwAQ-/0/1760267870162?e=1763596800&v=beta&t=3XzoLvd7E6rWZVAeOl3n1Djqyv9qPntJ84DpGxZC9jM align="left")

### **What are Falsy Values in JavaScript?**

In JavaScript, some values automatically convert to false when used in a Boolean context.

* false
    
* 0, 0, 0n (zero BigInt)
    
* "" (empty string)
    
* null
    
* undefined
    
* NaN
    

When you use this value in a condition, **JavaScript converts it to a Boolean**. If it’s a falsy value, the condition acts like false.

![Article content](https://media.licdn.com/dms/image/v2/D5612AQG-9iL_A1NmkQ/article-inline_image-shrink_1500_2232/B56ZnW_aIgIsAU-/0/1760248571495?e=1763596800&v=beta&t=RDX-cSKgHGl0XNs8RFMvBwrCm5XGmZK3MDgBRVdKjRA align="left")

None of these will print anything because all are falsy.

> That’s why if (!favoriteNumber) is dangerous; it doesn’t just catch null or undefined, it also catches 0, NaN, or "". That can be misleading

---

### **Why you should avoid using ! for Checking Presence? Why ! is misleading?**

Using !value to check if something exists or is valid can be misleading because it treats *all* falsy values as missing, even if some are valid inputs.

Consider this example again, checking a user's favorite number:

![Article content](https://media.licdn.com/dms/image/v2/D5612AQHy-JDKTMv7TQ/article-inline_image-shrink_1500_2232/B56ZnXALKCHkAU-/0/1760248772463?e=1763596800&v=beta&t=Jw1568wR6Uu-NgaKHVNUnI-Oexcz0FgJWrOP-WnHIDU align="left")

Here, !favoriteNumber is true if favoriteNumber is 0, an empty string, null, undefined, or NaN. This means you might reject valid inputs like 0.

### **Then what should you do? What is the solution?**

If your goal is to check whether a value is only **null or undefined**, use:

![Article content](https://media.licdn.com/dms/image/v2/D5612AQGWaDLjcIFZGw/article-inline_image-shrink_1500_2232/B56ZnXB4thIYAY-/0/1760249220716?e=1763596800&v=beta&t=uJRGxzakAw-SZFkO5QKtl4aIpksvUNGjzPhBSBL6aLc align="left")

Notice the **double equals (**\==) here and that’s intentional.

x == null is true for **both** null and undefined, but false for 0, "", or false. This is one of the few cases where using == is actually recommended.

Best solution for this problem :

![Article content](https://media.licdn.com/dms/image/v2/D5612AQExihyfg-VPFA/article-inline_image-shrink_1500_2232/B56ZnXCWYqH8AU-/0/1760249343085?e=1763596800&v=beta&t=IXrVgkSy_lzoQVNQzoWsqisqKkcbU3X7DOWpc4YchCw align="left")

> But why didn't I use === here? why used ==? Because we all know JavaScript is weird

---

### **Understanding == vs ===**

* \== (double equals) is **loose equality**: Checks if the values are the same, even if the types are different. It tries to convert types before comparing. Example: 5 == "5" → true
    
* \=== (triple equals) is **strict equality**: Checks if both the value and type are exactly the same. No type conversion. Example: 5 === "5" → false
    

But here is the twist. Example:

![Article content](https://media.licdn.com/dms/image/v2/D5612AQEqwzPpgM2p-w/article-inline_image-shrink_1500_2232/B56ZnXDF5TI4AU-/0/1760249536770?e=1763596800&v=beta&t=jSoQSl0maT2t6yi49drDsdyuS_ukJQbtApm0t_Uwe0Q align="left")

Here’s what happens:

1. JavaScript sees one side as a number and the other as a string.
    
2. It converts the empty string "" to a number, which becomes 0.
    
3. So the result is 0 == 0 → true.
    

> This is why using == blindly can cause bugs that are almost invisible.

Let' see another weird example :

![Article content](https://media.licdn.com/dms/image/v2/D5612AQGaU26DmXV31w/article-inline_image-shrink_1500_2232/B56ZnXD.mhKMAU-/0/1760249769516?e=1763596800&v=beta&t=wY_dfuM8CTiF16DT4KeYlVd0-f7I0fuW1bT-ooUIdWk align="left")

What's happening here!

1. \== treats null and undefined as equal. Also, 0 and " as equal
    
2. \=== checks both **type** and **value**, so it says they are different. same for 0 and " as different.
    

### **What is the solution? When to Use Which?**

* Use === most of the time: It avoids weird bugs by checking both value and type. Example: if (age === 18) { ... }
    
* Use == null only in special cases: It checks if a value is either null or undefined in one go. Example: if (userInput == null) { ... } . This is handy when you're checking for "missing" values.
    

> 💡 Rule of thumb: Always stick to === unless you have a specific reason to use == null.

The triple equals (===) operator **does not** perform type coercion. It checks value **and** type, so it’s more predictable.

![Article content](https://media.licdn.com/dms/image/v2/D5612AQG957PUv97HCg/article-inline_image-shrink_1000_1488/B56ZnXI8CDIAAQ-/0/1760251069307?e=1763596800&v=beta&t=oSOoYs-_b5EAeRTsgJyGRfQpE1W0u65eEjNGUvGBnr4 align="left")

> What is type coercion? **Type coercion** means JavaScript automatically converts a value from one data type to another when needed.

![Article content](https://media.licdn.com/dms/image/v2/D5612AQEkfi7TV-CnYQ/article-inline_image-shrink_1500_2232/B56ZnXJLaLHQAU-/0/1760251132429?e=1763596800&v=beta&t=cPzMhWQECXnOAIJC-mfy6YN6VvVBa3ToA5iv_Zdl-EM align="left")

> So, JavaScript tries to “help” by changing types behind the scenes which can lead to unexpected results.

So we are watching how the concept of JavaScript is weird!

Loose equality == can cause unexpected results due to JavaScript's type coercion. Strict equality === is generally safer because it avoids these surprises by requiring both type and value to be the same.

This consistency is why developers say:

> “Always use ===, unless you’re explicitly checking for both null and undefined, then use == null.”

![Article content](https://media.licdn.com/dms/image/v2/D5612AQGtlvlIbvIWqg/article-inline_image-shrink_1500_2232/B56ZnXFE5FIsAY-/0/1760250057206?e=1763596800&v=beta&t=1SayJCFvgomDVaoYEaCjkS06kUG9EOpgaij4XOq2TsU align="left")

---

### **Why not to use ! and rely on == too Much?**

The ! (logical NOT) operator converts the value to a Boolean and then negates it.

![Article content](https://media.licdn.com/dms/image/v2/D5612AQHqmJCCl1Cscw/article-inline_image-shrink_1500_2232/B56ZnXFVk3IsAU-/0/1760250125648?e=1763596800&v=beta&t=QAbWA1wYBDITCdQAGnScIjvj1Ag1IGAiot12b_AnUsI align="left")

That’s why using !value to check for “missing” data is unreliable. If you want to check whether a number exists and allow 0, !value will fail.

* !value converts the value to a Boolean first. Since many legitimate inputs like 0 or "" are falsy, this can cause errors.
    
* \== uses type coercion which can cause confusing results (like 0 == "" being true).
    
* \=== avoids coercion and thus helps prevent bugs.
    

---

### **Best Solution?**

Here’s the fixed version of our earlier function:

![Article content](https://media.licdn.com/dms/image/v2/D5612AQE_ycyxsrO51g/article-inline_image-shrink_1500_2232/B56ZnXFbpfKIAU-/0/1760250150719?e=1763596800&v=beta&t=K-0KP1ZtwxBXMK1eKvpfK9-HuhWZfbeGTemXPiIZGds align="left")

This now handles:

* 0 correctly as a valid number.
    
* Rejects null or undefined.
    
* Avoids bugs from falsy checks.
    

![Article content](https://media.licdn.com/dms/image/v2/D5612AQH6fbiddSsLzg/article-inline_image-shrink_1500_2232/B56ZnXFhTWHAAU-/0/1760250173769?e=1763596800&v=beta&t=0KvPiVBwjFEI63oJ_PKIZIkLlACO-QvXQomJ_m95Z1I align="left")

Try this in console of browser!

These tiny details are what make **JavaScript “weird,”** but once you understand them, you can use them with confidence.

### **Just Remember :**

1. **Don’t use** !value to check for missing data if 0, "", or NaN are valid.
    
2. **Use** x == null when you want to check for both null and undefined.
    
3. **Prefer** === in almost all comparisons to avoid type coercion surprises.
    
4. **Know the falsy values,** it explains most “weird” JavaScript behavior.
    
5. Always think twice before using shorthand conditions in logic checks.
    
6. Validate types explicitly when necessary.
    

![Article content](https://media.licdn.com/dms/image/v2/D5612AQHSQIQGA1wH3w/article-inline_image-shrink_1500_2232/B56ZnXIeW7JsAU-/0/1760250948464?e=1763596800&v=beta&t=iUap_Tw7NwAxl76uYK3HNMCY1XxSfvLo1pkc9xfnx-Q align="left")

JavaScript’s flexibility is what makes it fun, but also confusing at times. The !, ==, and === Operators seem simple, yet they can completely change the meaning of your code.Knowing when to use each one will save you from subtle bugs that take hours to track down.

---

**🧡 Thanks for Reading!**

That’s all! I hope you learned something new or saw tech from a new angle. Until next time, keep learning and building!

I regularly share what I learn through weekly posts on [**LinkedIn**](https://www.linkedin.com/in/sumonta-saha-mridul-b35bb61a0/), **Dev. to**, and **Medium**. Also, I run a small [**YouTube channel**](https://www.youtube.com/@LearnCodewithPS5638) where I try to share helpful content for developers.

***Sumonta Saha Mridul***\*, Associate Software Engineer I,\* [**Cefalo Bangladesh Ltd.**](https://www.linkedin.com/showcase/cefalobangladesh/)

* YouTube: [**Code & Career Golpo**](https://www.youtube.com/@codecareergolpo5638)
    
* Medium: [**Sumonta Saha Mridul**](https://medium.com/@sumontasaha80)
    
* Hashnode: [**Code & Career Golpo**](https://sumonta056.hashnode.dev/)
    

![Article content](https://media.licdn.com/dms/image/v2/D5612AQGWVU-wU_qh3g/article-inline_image-shrink_1000_1488/B56ZnYMMdOHAAQ-/0/1760268705814?e=1763596800&v=beta&t=mgGFoV1x_Ud3fX4-hBZYajcLOTJzzH3fItEeeQSZwrg align="left")