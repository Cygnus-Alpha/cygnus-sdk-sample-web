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
<script src="./chatbotSDK.umd.js"></script>
<link rel="stylesheet" href="./chatbot-sdk.css">
```

## Usage

### Initialize the Chatbot

To initialize the chatbot, call the `initialize` method with the ID of the container where the chatbot should be rendered and a settings object.

```html
<script>
  window.ChatbotSDK.initialize('sdk-container', {
    apiKey: 'your-api-key',
    apiEndpoint: 'your-api-endpoint',
    boxSize: { width: '400px', height: '500px' },
    position: 'top-left',
    logo: 'path/to/your/logo.png',
    themeName: 'green',
    customPayload: {
      page: 'dashboard',
    }
  });
</script>
```

### Configuration Settings

When initializing the chatbot, you must provide the following required settings:

- `apiKey` (string, **required**): Your API key for authentication.
- `apiEndpoint` (string, **required**): The endpoint URL for the chatbot API.
- `boxSize` (object, **required**): The dimensions of the chatbot box.
  - `width` (string): Width of the chatbot box, e.g., `'400px'`.
  - `height` (string): Height of the chatbot box, e.g., `'600px'`.

Optional settings include:

- `botName` (string, optional): The name of the bot.
- `themeColor` (string, optional): The primary color theme of the chatbot, e.g., `#ff5733`.
- `fontFamily` (string, optional): The font family to be used in the chatbot, e.g., `'Arial, sans-serif'`.
- `position` (string, optional): The position of the chatbot on the screen, Possible values are `'bottom-right', 'bottom-left', 'top-right', 'top-left'`.
- `logo` (string, optional): URL to the logo image to be displayed in the chatbot.
- `themeName` (ThemeName, optional): The name of the theme to be applied. Possible values are `"light"`, `"dark"`, `"blue"`, `"red"`.
- `enableLogger` (boolean, optional): Enable or disable logging, default is `false`.
- `customPayload` (object, optional): Additional data to be sent with each message.

Example:

```javascript
window.ChatbotSDK.initialize({
  apiKey: 'your-api-key',
  apiEndpoint: 'https://api.yourchatbot.com',
  botName: 'CygnusBot',
  themeColor: '#ff5733',
  fontFamily: 'Arial, sans-serif',
  boxSize: { width: '400px', height: '600px' },
  position: 'bottom-right',
  logo: 'https://example.com/logo.png',
  themeName: 'dark',
  enableLogger: true,
  customPayload: { userId: '12345' }
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
    <script src="https://unpkg.com/react@18/umd/react.development.js"></script>
    <script src="https://unpkg.com/react-dom@18/umd/react-dom.development.js"></script>
    <script src="./chatbotSDK.umd.js"></script>
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


