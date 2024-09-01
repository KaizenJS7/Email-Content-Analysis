<h1>Email Content Analysis</h1>

What lenguage does the email employ? Are there any indicators of social engineering tactics? How does the email appear when it's viewed in the client?

We can think of considerations like the content type, encoding, wording, or even grammer and formatting.

<h2>Sample 1</h2>

<img src="https://i.imgur.com/NtCjTOa.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />

So this is going to be the first email that we're looking at, and specifically let's also open this up in Sublime Text.

<img src="https://i.imgur.com/aqr9vlC.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />

<b>MIME-Version</b> 

<b>Mime-Version</b> is a standard email header that specifies the version of the MIME protocol used by the email message. MIME extends the format of email to support:


- Text in character sets other than ASCII
- Non-text attachments (like images, audio, video)
- Message bodies with multiple parts (e.g., a plain-text and an HTML version of an email)
- Header information in non-ASCII character sets

<img src="https://i.imgur.com/SXnbtyu.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />

<b>Content-Type</b>

The <b>Content-Type</b> header defines the type of data contained in the message or document, including its format and character set. It is crucial for rendering text, images, attachments, or any multimedia content correctly.

<img src="https://i.imgur.com/QZbJaNu.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />

<b>Content-Transfer-Encoding</b>

The <b>Content-Transfer-Encoding</b> header tells the email client how to decode the message body so that it can properly display or handle the content. Email was originally designed to handle plain text (ASCII characters), so any non-ASCII content (such as binary data, images, or files) must be encoded in a way that it can be safely transported over email protocols (like SMTP) which do not support all data formats natively.

1. <b>7bit:</b>

- Indicates that the content is ASCII text and is compatible with the original 7-bit SMTP.
- No encoding transformation is applied.
- Used for plain text messages that only contain standard ASCII characters.

2. <b>8bit:</b>

- Used for text that includes extended ASCII characters (values greater than 127) but no binary data.
- Requires an 8-bit clean channel for transmission, which may not be available on all email servers.

3. <b>binary:</b>

- Indicates that the content is raw binary data.
- Requires an 8-bit clean channel for transmission, and the data may not be altered or encoded.
- Not commonly used because many email servers do not support raw binary data transmission.

4. <b>base64:</b>

- Encodes binary data into ASCII characters.
- Commonly used for attachments like images, documents, or any binary data to ensure safe transmission over email.
- Converts every 3 bytes of binary data into 4 ASCII characters.

5. <b>quoted-printable:</b>

- Encodes text in a way that is mostly human-readable, used mainly for text that contains mostly ASCII characters but also some special characters (like UTF-8 encoded text).
- Non-printable ASCII characters are represented by a = followed by their hexadecimal value.

<img src="https://i.imgur.com/MuoinDq.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />

<b>MIME-Boundry</b>

The <b>MIME-Boundary</b> is a unique string specified within the Content-Type header of a MIME email to mark the boundaries between different parts of the email body. The email body is split into parts, each starting with a boundary line that begins with two hyphens (--) followed by the boundary string. The boundary string itself is usually chosen so that it does not appear anywhere in the actual content of the email.

<img src="https://i.imgur.com/bFHMRcE.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />

So the presence of two boundry strings (Lines 95 and 101) here indicates that the email contains two parts.

This is a common practice in MIME encoded emails, to provide an alternate presentation of the same content.

<img src="https://i.imgur.com/A0ispo4.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />

In this case, we don't have a plain text, all of it is under this HTML here.

<img src="https://i.imgur.com/5H2R6Re.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />

We can see the text HTML under the <b>Content-Type</b>, indicating that this is going to be HTML rendered content.

<h2>Going Back</h2>

Let's return to the email in the client.

<img src="https://i.imgur.com/NtCjTOa.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />

We can see some oddities right off the bat that might provide red flags that this isn't a legitimate email.

First off, the email is claiming to be from Trustwallet, a cryptocurrency trading platform. At first glance, I didn't know what Trustwallet was. But a simple Google search showed me that the organization that the email claims to be from is somewhat legitimate.

<img src="https://i.imgur.com/XqNiZeP.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />

However, the first thing noticed is that there is a discrepancy between how the company name is spelled in the email versus how the company name is actually spelled.

<img src="https://i.imgur.com/c29G6H3.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />

We can see in the email, well we don't have a space between Trust and Wallet, it's all one word. But the actual company is two words, Trust and Wallet.

<img src="https://i.imgur.com/nDw6zge.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />

There are also a couple of random grammer and spelling oddities in the email, such as the greeting. 

We can see <b>Hi Dear; Customer</b>, this appears to be a failed attempt at writting a generic greeting, since it sounds awkward and contains awkward punctuation.

Sometimes you'll see phishing emails that can actually parse and decipher a mailboxes associated name, such as Andrew or Bob or Emily. But in this case, less configuration was done on the attackers end to just give a generic customer greeting. 

The first line of the email here also indicates a potential attempt at including a sense of urgancy, claiming that we have an unverified account that will be suspended if we don't action the email. And of course, this isn't always a case closed kind of indicator, but seeing these type of social engineering tactics come to play should raise our suspicion and warrant further investigation. You'll often see this done with expiring accounts or claiming accounts will be suspended because in many cases, money and bank details are involved, like with bank and cryptocurrency exchanges. Well, victims might feel a heightened sense of urgency and quite easily click on malicious links.

<h2>Sample 2</h2>

<img src="https://i.imgur.com/HcFEnHf.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />

This also claims to be from Trust Wallet, and we can obviously go into the headers and almost immediately identify this as a spoofing or impersonation attempt, but let's just focus on the content.

This time, they seem to have typed the Trust Wallet name correct, but we're still getting a generic greeting with dear customer and a lot of poor grammar. 

For example, we can see the possessive accent here next to NFTs, which grammatically shouldn't be there as it's indicating a plurar.

<img src="https://i.imgur.com/YX8Ke0T.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />

Lastly, down here the word assistance is spelled incorrectly, indicating whoever wrote this email might not have English as their first lenguage. Being able to spot grammatical or spelling errors can quickly raise suspicion that an email did not come from a professional source. 

<img src="https://i.imgur.com/Pznoh46.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />

But on the other side, with things like AI and options like ChatGPT are becomeing so readily available, well attackers from around the world can quickly generate legitimate sounding copy for email, which is why this alone can't be our only barometer.

<h2>Sample 3</h2>

<img src="https://i.imgur.com/atMMXli.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />

In this case, we'll find a genuinely convincing looking body resembling an Amazon account suspension notice, and it uses all the correct formating, logos, and fonts. They likely copied this from a legitimate Amazon email. So you can imagine that someone who might have recently ordered something on Amazon, which of course is quite common these days, could receive this email and jump to conclusions out of fear and manipulation of authority. In this case, the content of this phish was done so well that we can''t just rely on content inspection alone and of course, we never should. So we'll need to look at other methods of analysis like header analysis and URL inspection.

<h2>Sample 4</h2>

<img src="https://i.imgur.com/x6LKl90.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />

Lets open this in Sublime Text

<img src="https://i.imgur.com/48I3pfq.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />

If we scroll down to the content of this email and we can also see it from the preview window at the right, we have a long block of Base 64 content. 

<img src="https://i.imgur.com/RYz1XIW.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />

We can use a tool like CypherChef to decode this for us.

<b>CypherChef (gchq.github.io/CyberChef/)</b>

<img src="https://i.imgur.com/bdA6JKs.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />

In the <b>Input</b> window, we can just paste in the contents.

<img src="https://i.imgur.com/DxgUvX2.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />

And if we go under <b>Operations</b>, if we do <b>From Base64</b>, we can see that "This operation decodes data from an  ASCII Base64 string back into its raw format"

So if we drag this over to our <b>Recipe</b> and let it go, well we can see in our <b>Output</b> that it was successfully decoded into HTML text.

<img src="https://i.imgur.com/CFjLcU1.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br 

So if we look at this, this is the actual HTML and CSS markup that made up our email.

<h2>HTML Entities</h2>


<img src="https://i.imgur.com/DVc5upe.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br 

Next, Let's cover another encoding mechanisim called HTML entity encoding, where in reality, this is really just a sequence of characters to represent specific HTML characters.
So HTML uses entities to display characters that are reserved for HTML syntax or characters that have specialized meanings, like the angle brackets, the less than and greater signs, or things like ampersands and non -breaking spaces.

For example if we go back to CypherChef, and if we just put an "&" symbol in the <B>Input</b> window, and we go under <b>Operations</b> and search for <b>To HTML Entity</b>, and if we drag over <b>To HTML Entity</b>, well this is going to convert characters into those HTML entities. We can see that our "&" symbol turned into this "<b>&amp</b>"

<img src="https://i.imgur.com/51sDNpu.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br 

For example, if I were to check off this convert all characters, well this is going to basically convert everything I type into HTML entities.

<img src="https://i.imgur.com/GdQTvtf.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br 

If I just type in "test", well we can see a number of HTML entities.

<img src="https://i.imgur.com/RyvVhWt.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br 

The "<b>&#116</b>" refers to the letter "t", "<b>&#101</b>" refers to the letter "e" and so on.

So attackers employ various techniques to buy pass spam filters. The use of HTML entities is one such method, and you can likely see how HTML entities can be leveraged.

For example, suppose we have a spam filter in place to reject or quarantine any emails that include the phrase Bitcoin.

<img src="https://i.imgur.com/mC3ylsS.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br 

In this scenerio, maybe our oranization has nothing to do with Bitcoin, and we've been seeing an uptick in cryptocurrency related scams. In this case, an attacker could just insert one of these entity characters to potentially bypass the spam filter, and I'll say any good quality filters will be able to decode this and performstatic analysis to catch this evasion attempt. 

<h2>URL Encoding</h2>

URL encoding is a method used to convert charactors into format that can be transmitted over the internet. This is often used for legitimate purposes, but an attacker may attempt to encode URLs to bypass some weaker spam filters. URL encoding works by replacing non alphanumeric characters with a percent sign followed by a two digit hexadecimal value that represents the character in the ASCII character set.  
For example let's paste the CypherCehf URL into the <b>Input</b> window and if we do a quick search in <b>Operations</b> for URL, well we should see <b>URL Encode</b> as an option. This is going to encode potentially problematic characters into that percent encoding.

<img src="https://i.imgur.com/TbbkvW3.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br 

So if we drag this over to ther <b>Recipe</b> and click on <b>Encode all special chars</b>, well we can see a number of those characters like the colon and the backlashes, have been transformed into that percent encoding.

<img src="https://i.imgur.com/dgX9npF.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br> 

<h2>Sample 5</h2>

If we open up Sample 5 in Sublime text, and hit "<b>CTRL+F</b>" we can search for "<b>%2E</b>"

<img src="https://i.imgur.com/vrx4fOx.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br 

We can see a long string of text that is both URL encoded and also HTML entity encoded and of course we can decode this using <b>CypherChef</b>.

So if I find where it ends based on the quotation and go all the way to where the URL starts based on the first quotation, I can just copy this.

<img src="https://i.imgur.com/RFIU9K1.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br 

Interestingly enough, if we scroll up here to the <b>Content-Transfer-Encoding</b>, we can also see that this content is encoded with the <b>quoted-printable</b>.

<img src="https://i.imgur.com/W9SzYco.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br 

So basically, that's three layers of encoding that we have here in that URL. So lets head back over to <b>CyberChef</b> and paste in that URL.

<img src="https://i.imgur.com/3nbP3uY.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br 

We can see it doesn't really look like a proper URL because it's been encoded using quoted printable. So first, let's look up in <b>Operations</b> the word <b>From Quoted Printable</b> option. Let's drag that over to our <b>Recipe</b>.

<img src="https://i.imgur.com/g22fn8J.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br 

We can see our URL is starting to look a little bit better, but remember we also have the HTML entity encoding, so let's look up that as well. 
If we search <b>From HTML Entity</b>, again we can drag it into our <b>Recipe</b>.

<img src="https://i.imgur.com/7roPs15.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br 

We can see that our URL was cleaned up a bit more. Lastly, let's look up <b>URL Decode</b> and drag that over, and we can finally get our full URL without any of that encoding.

<img src="https://i.imgur.com/n017PQV.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br 

Now that we have the URL decoded, we can now pass it over to some tools to conduct URL analysis.

<b>THIS WAS FOR EDUCATIONAL PURPOSES ONLY</b>
