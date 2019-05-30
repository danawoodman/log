# Software Development Practicies and Principles

## Development Process

### Code review is essential

### Use continuous integration

### Pull requests should be testable

If you do code review (which you absolutely should do), your Pull Requests should be testable meaning that you can take the code in question and run it in a real world test. For example, if it is a web app, the Pull Request should create an isolated deployment of the changes so a code reviewer can QA the work how it will actually be used. Just looking at code is often not enough to have confidence in code, especially complicated changes. The same should apply for APIs, mobile and desktop apps and other types of software. Use your CI to do this work for you automatically.
