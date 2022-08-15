# Traversing Nested Objects

## Learning Goals

- Revisit why nested objects are useful
- Practice accessing inner properties

## Introduction

Imagine you've just been onboarded to the dev team working on Flatbook, the world's
premier social network. Here at Flatbook, we have some
pretty complex data-modeling needs. For instance, think about the breadth of
information we might want to display on each user's profile page:

- First name
- Last name
- Employer
  - Company name
  - Job title
- Friends
  - First name
  - Last name
  - Employer
    - Company name
    - Job title
- Projects
  - Title
  - Description

We can already start to see some problems with trying to fit all of this into a
_shallow_ (non-nested) JavaScript object:

```js
const userInfo = {
  firstName: "Avi",
  lastName: "Flombaum",
  companyName: "Flatbook Labs",
  jobTitle: "Developer Apprentice",
  friend1firstName: "Nancy",
  friend1lastName: "Burgess",
  friend1companyName: "Flatbook Labs",
  friend1jobTitle: "Developer Apprentice",
  friend2firstName: "Corinna",
  friend2lastName: "Jackson",
  friend2companyName: "Flatbook Labs",
  friend2jobTitle: "Senior Developer",
  project1title: "Flatbook",
  project1description:
    "The world's premier social network.",
  project2title: "Scuber",
  project2description:
    "A burgeoning startup helping busy parents transport their children to and from all of their activities on scooters.",
};
```

Goodness, that's messy. It would be a nightmare to keep the object updated. If
Avi un-friends Nancy, do we shift Corinna's info into the `friend1...` slots and
delete the `friend2...` properties, or do we leave Corinna as `friend2...` and
delete the `friend1...` properties? There are no good answers. Except...

## Objects in Objects

Recall from the lesson on objects that the values in an object can be
_anything_, including another object. If we reorganize the above object a bit,
it becomes significantly easier to read and update:

```js
const userInfo = {
  firstName: "Avi",
  lastName: "Flombaum",
  company: {
    name: "Flatbook Labs",
    jobTitle: "Developer Apprentice",
  },
  friends: [
    {
      firstName: "Nancy",
      lastName: "Burgess",
      company: {
        name: "Flatbook Labs",
        jobTitle: "Developer Apprentice",
      },
    },
    {
      firstName: "Corinna",
      lastName: "Jackson",
      company: {
        name: "Flatbook Labs",
        jobTitle: "Lead Developer",
      },
    },
  ],
  projects: [
    {
      title: "Flatbook",
      description:
        "The premier Flatiron School-based social network in the world.",
    },
    {
      title: "Scuber",
      description:
        "A burgeoning startup helping busy parents transport their children to and from all of their activities on scooters.",
    },
  ],
};
```

We've pared the sixteen messy properties in our first attempt down to a svelte
five: `firstName`, `lastName`, `company`, `friends`, and `projects`. `company`
points at another object, and both `friends` and `projects` point to arrays of
objects. Let's practice accessing some of those beautifully nested data points.
Copy `userInfo` into the [replit][] code window and follow along. Once you click
run, you can check the values of the variable's properties in the console
window.

To review, for a property at the top level of our object, we can grab a value
using dot notation:

```js
userInfo.lastName;
//=> "Flombaum"
```

If the property we're accessing is nested inside another object, we just append
the additional key(s):

```js
userInfo.company.jobTitle;
//=> "Developer Apprentice"
```

If the property is nested inside an array, we need to specify the index in the
array for the object that we want. To get the first name of Avi's first friend
and the title of his second project:

```js
userInfo.friends[0].firstName;
//=> "Nancy"

userInfo.projects[1].title;
//=> "Scuber"
```

It's worth spending some time getting comfortable with nested data structures —
you will see a lot of them as you proceed through the curriculum and in your
career as a developer. Create your own in the REPL and practice accessing
various pieces of data.

## Conclusion

Structuring data can often be a daunting task, but nesting makes it more approachable
and readable. Being able to access nested data becomes very important in such cases. 
It can be confusing sometimes when data is nested several times over or when there are
multiple different data structures being used -- but the more you practice, the easier it
will become!

[replit]: https://replit.com/languages/javascript
[array-methods]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array#static_methods
[isarray]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/isArray
