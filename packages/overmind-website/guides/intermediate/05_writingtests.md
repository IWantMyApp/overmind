# Writing tests

Testing is a broad subject and everybody has an opinion on it. We can only show you how we think about testing in general and how to effectively write those tests for your Overmind app. It is encouraged to think **unit testing** of actions and effects. This will cover expected changes in state and that your side effects behaves in a predictable manner. If you want to test how your application works when it is all put together we recommend doing integration tests as close to the user experience as possible. Testing solutions like [Cypress.io](https://www.cypress.io/) is a great way to do exactly that.

## Testing actions

When testing an action you want to verify that changes to state are performed as expected. To give you the best possible testing experience Overmind has mocking tool called **createOvermindMock**. It takes your application configuration and allows you to run actions as if they were run from components.

```marksy
h(Example, { name: "guide/writingtests/action.ts" })
```

You might want to test if a thrown error is handled correctly here. This is an example of how you could do that:

```marksy
h(Example, { name: "guide/writingtests/actiontest.ts" })
```

If your actions can result in multiple scenarios a unit test is beneficial. But you will be surprised how straight forward the logic of your actions will become. Since effects are encouraged to be application specific you will most likely be testing those more than you will test any action.

You do not have to explicitly write the expected state. You can also use for example [jest]() for snapshot testing. The action will return a list of mutations performed and effects run. This is perfect for snapshot testing.

```marksy
h(Example, { name: "guide/writingtests/actionsnapshot.ts" })
```

In this scenario we would also ensure that the **isLoadingPost** state indeed flipped to *true* before moving to *false* at the end.

## Testing effects

Where you want to put in your effort is with the effects. This is where you have your chance to build a domain specific API for your actual application logic. The bridge between some generic tool and what your application actually wants to use it for. A simple example of this is doing requests. Maybe you want to use axios to reach your API, but you do not really care about testing that library. What you want to test is that it is used correctly when you use your application specific API. Lets look at an example:

```marksy
h(Example, { name: "guide/writingtests/effect.ts" })
```

Lets see how you could write a test for it:

```marksy
h(Example, { name: "guide/writingtests/effecttest.ts" })
```

Again, effects is where you typically have your most brittle logic. With the approach just explained you will have a good separation between your application logic and the brittle and "impure". In an Overmind app, especially written in Typescript, you get very far just testing your effects and then do integration tests for your application. But as mentioned in the introduction we all have very different opinions on this, at least the API allows testing to whatever degree you see fit.