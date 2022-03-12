# elarian-bulksms


https://elarian.hashnode.dev/getting-started-with-elarian-bulk-sms-api-for-nodejs-developers


Getting Started With Elarian Bulk SMS API for Node.js Developers
Elarian is a customer engagement framework that helps you build robust applications with the customer as the unit of abstraction.
Elarian's photo
Elarian
·
Dec 10, 2021
·

3 min read

By Ian Githungo

Elarian provides infrastructure for building reactive, scalable applications fast. At its core, Elarian is a customer data and automation platform, even as you perform basic actions such as sending messages or handling payments; this data encompasses communications, payments, and activities generated from sources such as websites and mobile apps.

Elarian's goal is to help developers build scalable applications without worrying about the underlying infrastructures.

Head to their website for more information about Elarian

Services provided by Elarian include:

    Messaging: Engage customers across multiple platforms using a unified platform such as:

        WhatsApp

        SMS

        Telegram

        Facebook Messenger

    Payments: Seamlessly send, receive, and organize payments across multiple platforms

    Customer: Access Unified customer data in realtime to personalize engagements

    Head to the Elarian dashboard and create an account

    Create an Organization dashboard

2021-10-18_10-31.png

2021-10-18_10-32.png

    Head to the settings page and generate your API key. settings 2021-10-18_10-34.png

    Click the Send Security Code Button. A code will be sent to the email you used to sign up for your account.

2021-10-24_10-46.png

Enter the security code and click the generate button.

Ensure that you copy the API key to the clipboard before leaving the settings page

2021-10-24_10-49.png

    Create a channel

Head to the channels tab to create a new channel.

2021-10-18_10-42.png

2021-10-18_10-43.png

2021-10-18_10-47.png

    Grab the appId,orgId

2021-10-18_10-54.png

also don't forget the apiKey that you copied on the clipboard.

    Initialize a node.js project with the following command npm init and install the following npm packages with npm install

        dotenv

        elarian

Paste the credentials into the .env config file 2021-10-18_11-09.png

app.js

const dotenv = require("dotenv");
dotenv.config({ path: "./.env" });
const { Elarian } = require("elarian");

const client = new Elarian({
  appId: process.env.APP_ID,
  orgId: process.env.ORG_ID,
  appId: process.env.APP_ID,
});

client
  .on("error", () => {
    console.log("App failed to connect");
  })
  .on("connected", async () => {
    console.log("App connected successfully");

    const customer = new client.Customer({
      number: "+2547********", // you can enter your number here
      provider: "cellular",
    });

    const reponse = await customer.sendMessage(
      {
        number: process.env.SMS_SHORT_CODE, // you can either use the SMS_SHORT_CODE or the ALPHANUMERIC here
        channel: "sms",
      },
      {
        body: {
          text: "Thank you for chosing Elarian",
        },
      }
    );
    console.log(response);
  })
  .connect();

You can also add a start script in the package.json file.

{
  "name": "elarian_sms_app",
  "version": "1.0.0",
  "description": "",
  "main": "app.js",
  "scripts": {
    "start": "node app.js"
  },
  "author": "",
  "license": "ISC",
  "dependencies": {
    "dotenv": "^10.0.0",
    "elarian": "^0.2.16"
  }
}

Run the SMS app with:

npm run start

You can now check out the Elarian emulator on the dashboard.

2021-10-18_11-12.png

2021-10-18_18-00.png

If you have been able to reach this section and can view the message on the emulator great job! 🙂

You have successfully integrated Elarian Bulk SMS API to your Node.js Application.

For an even thorough understanding of the API, please check out the Elarian documentation.
