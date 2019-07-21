---
layout: post
title:      "Tips and Tricks for React and Redux"
date:       2019-07-21 04:14:16 +0000
permalink:  tips_and_tricks_for_react_and_redux
---


I have just completed my final project for Flatiron School, an exciting moment in my new career path. I was tasked with building an app with a backend in Rails and a separate frontend in React and Redux. It, for the most part, was smooth sailing. I built an app called WikiTrash - a Wikipedia for knowledge on the responsible disposal and recycling of different items. However, there were a few road blocks that were surprisingly difficult to surmount. 

**Automatically moving the item card once it hits 10 yes or no votes**
To clarify, once an item gets 10 yes or no votes on the information submitted, it is either persisted into the database of WikiTrash as a verified item, or it is entirely removed from the database and from the site. Every click on yes or no would update the redux state, but because the state update was at a deep level, I simply could not get the component to rerender and instantly remove the card from the page.

I tried just about ever lifecycle method, calling different functions within them, trying conditional rerendering, and anything else I could think of. I tried getSnapShotBeforeUpdate() and calling it withing componentShouldUpdate(). I worked on the container and then on the card. Nothing would trigger a rerender and the only way I could get the component to update was to navigate away from the page and then return to it. Then I found a rarely used but very important React method: forceUpdate().

forceUpdate() does just what it says it does - it forces the component to update. You don't need to pass anything to it, you just need to call this.forceUpdate() at the appropriate place and it will update. I chose to use it inside of a method I've called "updateComponent()", and then passed that function down as a prop to the Item Cards. 

```
    updateContainer = () => {
      this.forceUpdate()
    }
		
		<UnverifiedItemCard item={item} upVoteItem={this.props.upVoteItem} downVoteItem={this.props.downVoteItem} updateContainer={this.updateContainer} />
```

All of the item cards on this page are there conditionally, based on the fact that they have received neither 10 yes votes not 10 no votes. Once they have 10 of either, they are removed. So for my purposes, I needed the component to rerender after every upvote or downvote click, to check that the item was not either moved to verified items or removed entirely. Within my handleDownVote() and handleUpVote() functions (which are called onClick), after calling my dispatch action I simply called this.props.updateContainer(), which would update the container rather than the individual component. 

```
  handleUpVote = (event) => {
    this.props.upVoteItem(this.props.item)
    this.props.updateContainer()
  }

  handleDownVote = (event) => {
    this.props.downVoteItem(this.props.item)
    this.props.updateContainer()
  }
```

**Making only one fetch request to the API and rendering different components when navigating**
This one is a little more simple. In my App.js component, I sent a fetch request to my API when the component would mount.

```
  componentDidMount() {
    this.props.fetchItems()
  }
```

At first, it was firing off that fetch request every time I navigated to a different location in the site. Again I tried whatever I could think of. I added a conditional statement to componentDidMount() to only call fetchItems() if redux state was empty, and again, nothing worked.

As it turns out, it is not only an option to us React's Link component, but imperative to navigating with rendering rather than calling and remounting. As soon as I changed my a tags to Link components, everything worked. My app would make one initital fetch request when first visiting, and then render different components from the React router.
