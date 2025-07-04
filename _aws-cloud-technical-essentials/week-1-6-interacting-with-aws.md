---
title: Interacting with AWS
course: aws-cloud-technical-essentials-week-1
order: 6
layout: aws_post
---


### ইনফ্রাস্ট্রাকচারের ধরন বদলালে কাজ করার ধরনও বদলায়

যখন আপনি নিজের ইনফ্রাস্ট্রাকচারের মালিক, তখন তার সঙ্গে কিভাবে কাজ করতে হবে তা বোঝা সহজ। কারণ আপনি সেটাকে দেখতে পারেন, ছুঁতে পারেন এবং সরাসরি কাজ করতে পারেন।

যেমন, যদি আমি আমার আলমারিতে একটি সার্ভার বসাই, তাহলে সেই সার্ভারের সঙ্গে ইন্টারঅ্যাক্ট করাটা খুব সহজ—কারণ সেটা আমার নিজের, আমি সেটাকে ছুঁতে পারি।

কিন্তু যখন আমি কোনো কিছুকে ছুঁতে বা দেখতে পারি না—যেমন ধরুন, ইনফ্রাস্ট্রাকচার ভার্চুয়াল হয়ে গেলে—তখন তার সঙ্গে কাজ করার পদ্ধতিও একটু বদলে যায়।
এখন আমাকে আর শারীরিকভাবে কিছু করতে হয় না, বরং **AWS-এর API (Application Program Interface)** ব্যবহার করে **লজিক্যালভাবে** ইনফ্রাস্ট্রাকচার পরিচালনা করতে হয়।

এখন যখনই আমি কোনো AWS রিসোর্স তৈরি, পরিবর্তন বা মুছে ফেলি—হোক সেটা একটি ভার্চুয়াল সার্ভার বা এমপ্লয়িদের ছবির জন্য একটি স্টোরেজ সিস্টেম—আমি সেটি API কলের মাধ্যমে করি।

---

### **API কল করার তিনটি মূল উপায়**

AWS-এ API কল করার বেশ কয়েকটি উপায় রয়েছে, কিন্তু এই কোর্সে আমরা মূলত তিনটি নিয়ে কথা বলব:

1. **AWS Management Console**
2. **AWS Command Line Interface (CLI)**
3. **AWS Software Development Kits (SDKs)**

---

### **১. AWS Management Console**

নতুনরা যখন AWS ব্যবহার শুরু করেন, তারা সাধারণত **AWS Management Console** দিয়ে শুরু করেন।
এটি একটি ওয়েব-ভিত্তিক পদ্ধতি—যেখানে আপনি ব্রাউজার থেকে লগইন করে সরাসরি কাজ করতে পারেন।

এর সবচেয়ে বড় সুবিধা হলো—**পয়েন্ট অ্যান্ড ক্লিক** করে কাজ করা যায়।
মানে, কোনো সার্ভিস সম্পর্কে আগের জ্ঞান ছাড়াও আপনি শুধু ক্লিক করে ও প্রম্পট ফলো করে সহজেই শুরু করতে পারেন।
এখানে কোডিং বা সঠিক সিনট্যাক্স জানার দরকার নেই।

কনসোলে লগইন করলে, আপনি একটি **ল্যান্ডিং পেজ** দেখবেন যেখানে আপনার সম্প্রতি ব্যবহৃত সার্ভিসগুলো থাকবে।
আপনি চাইলে সব সার্ভিসও দেখতে পারবেন—যেগুলো **ক্যাটাগরি অনুযায়ী** সাজানো থাকে: যেমন **Compute**, **Database**, **Storage** ইত্যাদি।

ধরুন আপনি Region চেঞ্জ করে **Paris Region**-এ যান, তাহলে আপনি `eu-west-3.console.aws.amazon.com`-এ রিকোয়েস্ট পাঠাচ্ছেন—এটি Paris Region-এর Web Console।

যদিও কনসোল ব্যবহার শুরুতে খুব সহজ, কিন্তু একসময় আপনি বুঝবেন যে ম্যানুয়ালি রিসোর্স তৈরি করতে গেলে অনেক ধাপ পেরোতে হয়, এবং সেটা সময়সাপেক্ষ।

উদাহরণ: একটি Virtual Machine তৈরি করতে গেলে আপনাকে অনেকগুলো স্ক্রিনে গিয়ে কনফিগারেশন সেট করতে হয়।
একই জিনিস দ্বিতীয়বার করতে হলে আবার সেই পুরো প্রক্রিয়া ফলো করতে হবে। এতে **মানবিক ভুলের সুযোগ** বেড়ে যায়—একটি চেকবক্স ভুলে যাওয়া, বানান ভুল, কিংবা প্রয়োজনীয় সেটিংস বাদ দেওয়া।

---

### **২. AWS Command Line Interface (CLI)**

AWS ভালোভাবে বোঝা শুরু করলে, অথবা যদি আপনি এমন প্রোডাকশন এনভায়রনমেন্টে কাজ করেন যেখানে **রিস্ক ম্যানেজমেন্ট গুরুত্বপূর্ণ**, তখন আপনি এমন টুল ব্যবহার করতে চাইবেন যা আপনাকে **স্ক্রিপ্টিং বা প্রোগ্রামিং** করে API কল করতে দেয়।

**AWS CLI** হলো এমন একটি টুল।

দুটি উপায়ে এটি ব্যবহার করা যায়:

1. CLI ডাউনলোড করে আপনার কম্পিউটারে টার্মিনাল ব্যবহার করে
2. **AWS CloudShell** ব্যবহার করে, যেটি কনসোল থেকেই চালানো যায়

এখানে আপনি গ্রাফিকাল ইউজার ইন্টারফেস (GUI) এর পরিবর্তে **AWS সিনট্যাক্স** ব্যবহার করে কমান্ড চালান।

**উদাহরণ:** ধরুন, আমি CloudShell দিয়ে একটি ভার্চুয়াল মেশিন চালু করতে চাই।

* আমি প্রথমে কুইক শর্টকাট দিয়ে CloudShell চালু করব
* তারপর আমি টাইপ করব: `aws` → এর মাধ্যমে বুঝানো হয় API-এর সঙ্গে ইন্টারঅ্যাক্ট করা শুরু
* এরপর সার্ভিসের নাম—এই ক্ষেত্রে `ec2`
* তারপর সেই সার্ভিসে যা করতে চাই সেই কমান্ড ও প্রয়োজনীয় কনফিগারেশন

**CLI-এ একটি কমান্ড চালিয়ে** আপনি যা কনসোলে অনেক স্ক্রিন ঘুরে করেন, সেটি অনেক দ্রুত এবং নির্ভুলভাবে করা যায়।

তবে এক্ষেত্রে আপনাকে সঠিক সিনট্যাক্স জানতে হবে, এবং শুরুতে কিছুটা শেখার প্রয়োজন হয়। কিন্তু একবার স্ক্রিপ্ট লিখে ফেললে, তা বারবার চালানো যায়—যা অনেক সময় বাঁচায় এবং উৎপাদনশীলতা বাড়ায়।

---

### **৩. AWS SDKs (Software Development Kits)**

আপনি যদি **পুরোপুরি প্রোগ্রাম্যাটিক উপায়ে AWS API**-এর সঙ্গে কাজ করতে চান, তাহলে AWS SDK ব্যবহার করতে পারেন।

SDK হচ্ছে AWS কর্তৃক তৈরি ও রক্ষণাবেক্ষিত টুলসেট—যা জনপ্রিয় প্রোগ্রামিং ভাষায় পাওয়া যায়:
**Python**, **Java**, **Node.js**, **.NET**, **Ruby** এবং আরও অনেক।

আপনি যদি আপনার অ্যাপ্লিকেশন কোডকে AWS সার্ভিসের সঙ্গে ইন্টিগ্রেট করতে চান, তাহলে SDK অনেক উপকারী।

**উদাহরণ:**
আমাদের Employee Directory অ্যাপ্লিকেশনটি Python ও Flask দিয়ে তৈরি।
আমি চাইলে SDK ব্যবহার করে **Employee Photos** AWS স্টোরেজ সার্ভিসে পাঠাতে পারি।

কারণ SDK দিয়ে আপনি কোডের মধ্যেই **শর্ত (conditions), লুপ, অ্যারে, লিস্ট** ইত্যাদি প্রোগ্রামিং এলিমেন্ট ব্যবহার করে AWS রিসোর্স নিয়ন্ত্রণ করতে পারেন—এতে করে অনেক **সৃজনশীলতা ও ক্ষমতা** আসে।

---

### **সারসংক্ষেপ (Recap):**

AWS-এর সঙ্গে কাজ করার তিনটি প্রধান উপায়:

1. **AWS Management Console** – শুরু করার জন্য সহজ, পয়েন্ট-অ্যান্ড-ক্লিক পদ্ধতি
2. **AWS CLI** – টার্মিনাল/CloudShell-এ সিনট্যাক্স দিয়ে দ্রুত ও নির্ভুল কাজ
3. **AWS SDKs** – কোডের মাধ্যমে প্রোগ্রাম্যাটিকভাবে কাজ করার ক্ষমতা

এই কোর্সে আমরা প্রধানত **Console ব্যবহার** করব সার্ভিসের সঙ্গে কাজ করতে। তবে আপনি যদি আগ্রহী হন এবং একটু বেশি অভিজ্ঞ হন, তাহলে **CLI ব্যবহার করে নিজেকে চ্যালেঞ্জ** করতে পারেন।
