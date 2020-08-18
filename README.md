# DiscordWebhook-PHP
Easily send embedded/plain message.

Coded on phone - 8/16/20

# Usage
Include `DiscordWebhook.php` to your project then 
create an instance of the class.
```php
$dw = new DiscordWebhook("botName", "botAvatar.jpg", "WEBHOOK_URL");
```
You can also do this
```php
new DiscordWebhook("botName", "botAvatar");
new DiscordWebhook("botName", "WEBHOOK_URL");
new DiscordWebhook("botName");
new DiscordWebhook("botIcon");
new DiscordWebhook("WEBHOOK_URL");
new DiscordWebhook();
# You can set the webhook later if you send a message
```

## Send embedded message 

##### Single embed
```php
// You need to pass an ID to access your embed object because you can also create more embed object.
// Embed Id starts with #
$embed = $dw->embed("#embedId");

// and now set what you want
$embed["title"] = "Title of embed";
$embed["description"] = "Description of embed";
$embed["color"] = 1752220;

// then push the embed
$dw->push("#embedId", $embed);

// and finally send it
$res = $dw->send("#embedId");

// $res contains ["success" => boolean, "response" => actual_response_from_discord, "statusCode" => 200]

// You can also use callback
$dw->send("#embedId", function($success, $response, $statusCode) {
 // Do something
});

// and set webhook
$dw->send("#embedId", "WEBHOOK_URL");
```

![Preview](images/em_s.jpg)

##### Multiple embed
```php
$embed = $dw->embed("#embedId", 2); // 2 object is created and returned

$e1 = $embed[0]; // Access first embed
$e1["title"] = "Title embed of first embed";

$e2 = $embed[1]; // Access second embed
$e2["title"] = "Title embed of second embed";

// then push them
$dw->push("#embedId", $e1, $e2);

$dw->send("#embedId");
```

![Preview](images/em_m.jpg)

## Send plain message

```php
$dw->send("Message here!", "WEBHOOK_HERE_OPTIONAL");
```

![Preview](images/pm.jpg)


## More example
```php
$icon = "https://www.seekpng.com/png/full/20-205511_discord-transparent-staff-discord-logo-black-and-white.png";
$image = "https://discord.com/assets/f72fbed55baa5642d5a0348bab7d7226.png";
$webhook = "WEBHOOK_URL";

$dw = new DiscordWebhook("Discordy", $icon, $webhook);

$dw->newEmbed()
->setContent("Content above the embed")
->setTitle("Title of embed", "https://discordy.site")
->setDescription("Description of embed")
->setColor(1752220)
->setTimestamp(date("c", time()))
->setAuthor("Author name", "https://author.site", $icon)
->setImage($image)
->setThumbnail($icon)
->setFooter("Footer text", $icon)
->addField("Field 1", "field 1 value")
->addField("Field 2", "field 2 value")
->addField("Field 3", "field 3 value")
->send();
```

![Preview](images/e1.jpg)


