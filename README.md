# tiktok_auto.py
import os
import random
import requests
import schedule
import time

# Viral content templates (no OpenAI needed)
VIRAL_TEMPLATES = [
    "This {trend} hack will blow your mind! 🤯 #viral #trending",
    "I tried {trend} for 24 hours... here's what happened! 🚀",
    "5 {niche} secrets professionals don't want you to know! 🔥",
    "How to {trend} like a pro in 60 seconds! ⏱️",
    "The {trend} challenge you NEED to try! 💪"
]

TRENDS = ["AI", "viral", "Dubai", "tech", "money", "fitness"]
NICHES = ["marketing", "entrepreneurship", "coding", "investing"]

def generate_viral_content():
    trend = random.choice(TRENDS)
    niche = random.choice(NICHES)
    template = random.choice(VIRAL_TEMPLATES)
    return template.format(trend=trend, niche=niche)

def post_to_tiktok(caption):
    headers = {"Cookie": f"sessionid={os.getenv('TIKTOK_SESSION_ID')}"}
    # Add your actual video posting logic here
    print(f"Posting to TikTok: {caption}")
    # return requests.post("https://www.tiktok.com/api/video/upload", 
    #                     headers=headers, 
    #                     data={"description": caption}).json()

def daily_task():
    content = generate_viral_content()
    print(f"Generated content: {content}")
    post_to_tiktok(content)

# Schedule daily posting at 9 AM and 5 PM
schedule.every().day.at("09:00").do(daily_task)
schedule.every().day.at("17:00").do(daily_task)

print("TikTok Viral Bot Running...")
while True:
    schedule.run_pending()
    time.sleep(60)
