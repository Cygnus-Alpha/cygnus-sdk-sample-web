# Cygnus Chatbot SDK

The Cygnus Chatbot SDK is a powerful tool for integrating a chatbot into your web application. It provides functionalities for initializing the chatbot, managing user sessions, and handling messaging events.

## Features

- **Initialize Chatbot**: Easily set up the chatbot in a specified container.
- **User Management**: Set, get, and log out users.
- **Messaging Callbacks**: Define actions before and after sending messages, and when messages are received.
- **Send Messages**: Communicate with the chatbot programmatically.

## Installation

Include the SDK in your HTML file:

```html
<script src="./ca-assistant.umd.js"></script>
<link rel="stylesheet" href="./ca-assistant.css" />
```

## Usage

### Initialize the Chatbot

To initialize the chatbot, call the `initialize` method with the ID of the container where the chatbot should be rendered and a settings object.

```html
<script>
  window.ChatbotSDK.initialize('sdk-container', {
    apiKey: 'your-api-key',
    apiEndpoint: 'your-api-endpoint',
    responseCard: {
      titleFont: '18px',
      contentFont: '14px',
    },
    position: 'top-left',
    logo: 'path/to/your/logo.png',
    botIcon: 'path/to/your/logo.png',
    chatIcon: 'path/to/your/logo.png',
    chatFontSize: '16px',
    chatFontFamily: 'Gill Sans',
    themeName: 'dark',
    customPayload: {
      page: 'dashboard',
    },
  });
</script>
```

### Configuration Settings

When initializing the chatbot, you must provide the following required settings:

- `apiKey` (string, **required**): Your API key for authentication.
- `apiEndpoint` (string, **required**): The endpoint URL for the chatbot API.

Optional settings include:

- `responseCard` (object): The configuration for the response card inside the chatbot, where messages or responses are displayed.
  - `titleFont` (string): Specifies the font size for the title inside the response card, e.g., `'18px'`. It can be specified in various units such as px, em, rem, etc.
  - `contentFont` (string): Defines the font size for the content (the main body text) inside the response card, e.g., `'14px'`. It can be specified in various units such as px, em, rem, etc.
- `themeColor` (string, optional): The primary color theme of the chatbot, e.g., `#ff5733`.
- `chatFontFamily` (string, optional): The font family to be used in the chatbot, e.g., `'Gill Sans'`.
- `chatFontSize` (string, optional): The font family to be used in the chatbot, e.g., `'14px'`. It can be specified in various units such as px, em, rem, etc.
- `position` (string, optional): The position of the chatbot on the screen, Possible values are `'bottom-right', 'bottom-left', 'top-right', 'top-left'`.
- `logo` (string, optional): URL to the logo image to be displayed in the chatbot.
- `botIcon` (string, optional): The icon that represents the chatbot itself. This icon is typically displayed as a button that, when clicked, opens the chatbot interface. It's usually shown in a fixed position on the screen, often at the bottom right, to trigger the opening of the chat window.
- `chatIcon` (string, optional): The icon that appears in the chat window when a response is received.
- `themeName` (ThemeName, optional): The name of the theme to be applied. Possible values are `"light"`, `"dark"`, `"blue"`, `"red"`.
- `enableLogger` (boolean, optional): Enable or disable logging, default is `false`.
- `customPayload` (object, optional): Additional data to be sent with each message.

Example:

```javascript
window.ChatbotSDK.initialize({
  apiKey: 'your-api-key',
  apiEndpoint: 'https://api.yourchatbot.com',
  themeColor: '#ff5733',
  responseCard: {
    titleFont: '18px',
    contentFont: '14px',
  },
  position: 'bottom-right',
  logo: 'https://example.com/logo.png',
  botIcon: 'path/to/your/logo.png',
  chatIcon: 'path/to/your/logo.png',
  chatFontSize: '16px',
  chatFontFamily: 'Gill Sans',
  themeName: 'dark',
  enableLogger: true,
  customPayload: { userId: '12345' },
});
```

### User Management

#### Set User

Set the user information using the `setUser` method.

```javascript
window.ChatbotSDK.setUser({
  id: '123',
  name: 'John Doe',
  email: 'john.doe@example.com',
  token: 'user-token',
});
```

Set dynamic payload

```javascript
window.ChatbotSDK.dynamicPayload({
  api_auth_token: 'api_auth_token',
});
```

#### Get User

Retrieve the current user information.

```javascript
const user = window.ChatbotSDK.getUser();
console.log('Current user:', user);
```

#### Log Out User

Log out the current user.

```javascript
window.ChatbotSDK.setLogout();
```

#### Check User Login Status

Check if a user is logged in.

```javascript
const isLoggedIn = window.ChatbotSDK.isUserLoggedIn();
console.log('Is user logged in:', isLoggedIn);
```

### Messaging Callbacks

#### Before Sending a Message

Set a callback to execute before sending a message.

```javascript
window.ChatbotSDK.beforeSendMessage(() => {
  console.log('Preparing to send a message...');
});
```

#### After Sending a Message

Set a callback to execute after a message is sent.

```javascript
window.ChatbotSDK.afterSendMessage(() => {
  console.log('Message sent successfully.');
});
```

#### On Message Received

Set a callback to execute when a message is received.

```javascript
window.ChatbotSDK.onMessageReceived((message) => {
  console.log('Received message:', message);
});
```

### Send a Message

Send a message to the chatbot.

```javascript
window.ChatbotSDK.sendMessage(
  'Hello, chatbot!',
  (loading) => console.log('Loading:', loading),
  (isActive) => console.log('Chat active:', isActive),
  (messages) => console.log('Messages:', messages)
);
```

## Example

Here's a complete example of how to use the SDK in an HTML file:

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Chatbot SDK Integration</title>
    <script src="./ca-assistant.umd.js"></script>
  </head>
  <body>
    <div id="sdk-container"></div>
    <script>
      window.ChatbotSDK.initialize('sdk-container');
      window.ChatbotSDK.setUser({
        id: '123',
        name: 'John Doe',
        email: 'john.doe@example.com',
        token: 'user-token',
      });
      const isLoggedIn = window.ChatbotSDK.isUserLoggedIn();
      console.log('Is user logged in:', isLoggedIn);
      window.ChatbotSDK.beforeSendMessage(() => {
        console.log('Preparing to send a message...');
      });
      window.ChatbotSDK.afterSendMessage(() => {
        console.log('Message sent successfully.');
      });
      window.ChatbotSDK.onMessageReceived((message) => {
        console.log('Received message:', message);
      });
      window.ChatbotSDK.sendMessage(
        'Hello, chatbot!',
        (loading) => console.log('Loading:', loading),
        (isActive) => console.log('Chat active:', isActive),
        (messages) => console.log('Messages:', messages)
      );
    </script>
  </body>
</html>
```

## License

This project is licensed under the MIT License.
