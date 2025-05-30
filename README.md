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
    showWaitingMessages: true,
    waitingMessages: {
      initial: {
        time: 1,
        message:
          'Hold on! We are just adding the secret sauce to your experience.',
      },
      mid: {
        time: 5,
        message:
          'Taking a little longer, just adding the right flavor. Good things make you wait.',
      },
      late: {
        time: 10,
        message:
          'Yikes!! Seems our servers have also gone for a coffee break. Want to give it another go?',
      },
    },
    initialInfoText: 'Hello user how are you?',
    initialPrompts: ['Test A', 'Test B', 'Test C', 'Test D'],
    initialCameraPrompts: ['Test A', 'Test B'],
    showLoaderOnly: true,
    customBanner: `<div>HTML code</div>`,
    customPayload: {
      page: 'dashboard',
    },
    customPrompt: [
      {
        label: 'Hello user',
        value: 'Hello user How are you?',
        action: 'copy' | 'submit',
        showCameraIcon: false,
      },
    ],
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
- `showWaitingMessages` (boolean, optional): Show or hide the waiting messages, default is `false`.
- `waitingMessages` (object, optional): Custom messages to be displayed while the chatbot is processing the message. `waitingMessages` is an object with three properties: `initial`, `mid`, and `late`. Each property is an object with two properties: `time` and `message`. The `time` property is the number of seconds to wait before displaying the message. The `message` property is the message to be displayed.
- `initialInfoText` A custom message that will be displayed when the chatbot is first initialized, such as a greeting.
- `initialPrompts` Predefined response options for the user. These are likely shown as buttons or suggestions within the chat.
- `initialCameraPrompts` This can be a specific set of prompts related to the camera or capturing images, possibly shown to the user if the bot needs to interact with the camera.
- `showLoaderOnly` A setting to control whether only a loader (like a loading spinner or indicator) is shown to the user while waiting for a response.
- `customBanner` Custom HTML code for a banner that might be displayed within the chatbot interface, offering flexibility to include more advanced layouts or content like images, links, or special styling.
- `enableLogger` (boolean, optional): Enable or disable logging, default is `false`.
- `customPayload` (object, optional): Additional data to be sent with each message.
- `customPrompt` (Aray of object, optional): this is an array of objects, meaning you can have multiple objects within the array, each representing a different prompt with its own settings.
  Label: This refers to how the prompt will be displayed to the user.
  Value: This is the text message that will be sent when the prompt is selected.
  Action: There are two options here:
  Copy: The message will be copied to the input field.
  Submit: The message will be sent directly.
  showCameraIcon: If set to true, the camera icon will be shown; if set to false, the camera icon will not be shown.

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
  botName: '',
  showWaitingMessages: true,
  waitingMessages: {
    initial: {
      time: 1,
      message:
        'Hold on! We are just adding the secret sauce to your experience.',
    },
    mid: {
      time: 5,
      message:
        'Taking a little longer, just adding the right flavor. Good things make you wait.',
    },
    late: {
      time: 10,
      message:
        'Yikes!! Seems our servers have also gone for a coffee break. Want to give it another go?',
    },
  },
  initialInfoText: 'Hello user how are you?',
  initialPrompts: ['Test A', 'Test B', 'Test C', 'Test D'],
  initialCameraPrompts: ['Test A', 'Test B'],
  showLoaderOnly: true,
  headerInfoText: 'text';
  botIconText: 'text';
  cameraIcon: '/img/link';
  attachmentsIcon: 'img/link';
  autoSendPrompts: true;
  customBanner: `<div>HTML code</div>`,
  customPayload: { userId: '12345' },
  customPrompt: [
      {
        label: 'Hello user',
        value: 'Hello user How are you?',
        action: 'copy' | 'submit',
        showCameraIcon: false,
      },
    ],
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
