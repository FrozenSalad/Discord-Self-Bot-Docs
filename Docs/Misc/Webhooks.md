# Discord Webhooks

### Intro
Just a quick demo on how to use webhooks from a normal script

## Utilization
```py
import discord
import aiohttp

async def web():
    async with aiohttp.ClientSession() as session:
        # Put your webhook url
        url = ""
        webhook = discord.Webhook.from_url(url=url, session=session)
        await webhook.send("hi")
```
<br>

**In terms of how you can use this, webhooks essentially can send all messages including embeds and buttons**

```py
@bot.command()
async def test(ctx):
    await web(ctx)

async def web(ctx):
    async with aiohttp.ClientSession() as session:
        # Put your webhook url
        url = ""
        webhook = discord.Webhook.from_url(url=url, session=session)
        # Set your embed how you want
        embed = discord.Embed(
            title="Hello!",
            description="This is my description! Yippee!",
            color=discord.Color.green()
        )
        # Set the author, footer, and thumbnail/image
        embed.set_author(name=f"{bot.user.name}", icon_url=bot.user.avatar.url, url=bot.user.avatar.url)
        await webhook.send(embed=embed)


# You can even just straight up copy an application's embed and send it to a different channel witb a webhook

@bot.event
async def on_message(message: discord.Message):
    if message.embeds:
        for embed in message.embeds:
            if embed:
                await web(embed)
    
async def web(embed):
    async with aiohttp.ClientSession() as session:
        url = ""
        webhook = discord.Webhook.from_url(url=url, session=session)
        copy = embed.copy()
        await webhook.send(embed=copy)
```
