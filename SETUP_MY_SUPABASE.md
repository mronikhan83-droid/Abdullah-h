# আপনার Supabase সেটআপ (ধাপে ধাপে)

প্রজেক্ট ref: `ilglrxtbknldqclzxnyg`  — `.env` ইতিমধ্যে সেট করা আছে।
**শুধু `.env`-এর `SUPER_ADMIN_EMAIL` নিজের ইমেইল দিয়ে বদলান।**

## কম্পিউটারে (Node.js + Flutter লাগবে)
```bash
npm install -g supabase
supabase login
supabase link --project-ref ilglrxtbknldqclzxnyg   # DB password চাইবে
supabase db push                                    # সব টেবিল/RLS তৈরি হবে

supabase functions deploy create-user
supabase functions deploy admin-reset-password
supabase functions deploy compute-exam-stats
supabase functions deploy ai-gateway
supabase functions deploy health

# AI চাইলে (ঐচ্ছিক):
# supabase secrets set DEEPSEEK_API=... CLAUDE_API_KEY=...

flutter pub get
dart run build_runner build --delete-conflicting-outputs
flutter run            # ওয়েবে: flutter run -d chrome
```

## প্রথম একাউন্ট
Supabase Dashboard → Authentication → Users → Add user
→ `.env`-এর SUPER_ADMIN_EMAIL-এর ইমেইল + পাসওয়ার্ড, "Auto confirm user" টিক দিন।
তারপর অ্যাপে ওই ইমেইলে লগইন করুন।

## সমস্যা হলে
- লগইনে "Invalid API key" এলে: Supabase → Settings → API Keys → **Legacy** ট্যাব থেকে
  `eyJ...` anon key নিয়ে `.env`-এর `SUPABASE_ANON_KEY`-এ বসান।
- `SUPABASE_URL is not configured` এলে: `.env` প্রজেক্টের রুটে আছে কি দেখুন।
- `.disabled` শেষ হওয়া migration ফাইলগুলো ইচ্ছা করে বন্ধ রাখা, চালু করবেন না।
