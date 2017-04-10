---
published: true
title: The Bullshit Metric of Code Coverage
tags: 'specs, tests'
layout: post
---
Tests. Writing them sucks. Writing them is also probably the most important part of writing real, production quality code. We sacrificed the type safety of more boring languages like Java for the simplicity of Ruby code, and the price that decision is having to write a lot of tests.

Rails tests are especially bad. I've yet to read a Rails test that didn't have 3+ lines of mocking/setup for every expectation or assertion. It's the price of entry when your framework magics up half of your application.

And you know what else? Reading tests sucks, for most of the same reason that writing tests does. I can usually review a controller or service PR and follow the app code without any issues. But as soon as I get to that `spec/` folder, I go cross-eyed and lose all ability to judge anything but syntax and style guide issues. I just cannot get into the frame of mind I need to really digest the tests and figure out what cases are and aren't covered. And judging by other comments I see on PRs, I'm not the only one.

So. People hate writing tests. People hate reading tests. But tests are important, so we need some way to judge them. After what I assume was many navel-gazing sessions, people decided on code coverage. Everyone is hooked on 100% code coverage. Go look at open source repos on Github. One of the first thing in the readme is usually a little code coverage badge proudly exclaiming 100% coverage. And if you're below 100%? It turns into a scarlet badge of shame. I've judged repos for having less than 100% coverage before, and I know I'm not the only one.

The main repo I work on is at 100% coverage, and it will fail the build if it drops. Every line of code is run at least once in this test suite. So I should be free from bullshit bugs. I should never deploy code and feel my stomach drop as the error rate climbs from every third request hitting me code throwing a `NoMethodError` because of a nil. I mean, my code is tested. The code surrounding my code is tested. There's even a little badge telling me that.

But code coverage is bullshit. Doubly so in Rails. In this repo with over 1800 files in source control, I can run `expect(true).to be_truthy` in a single example and get over 50% code coverage. As soon as I load up Poltergeist and load my root route, I can push that over 60%. All of this without testing anything, really.

Code coverage's only value is in showing that you didn't forget a branch of logic. But it doesn't do shit to tell you about the quality of your tests. Can we agree on that?
