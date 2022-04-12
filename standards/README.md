## We prefer fewer, simpler standards
We want to:
- avoid creating an overwhelming body of standards that becomes difficult to keep track of and 
- spend as little time and effort as is viable reading and learning standards.


## Lifecycle of a standard
![](../assets/img/standard-lifecycle.png)

***NOTE:** Proposals can represent a new standard or an amendment or repeal of an existing standard.*

Proposals must include:
- a succinct summary,
- reasoning for the proposed change,
- an example/instructions on how to embody the standard unless repealing, and
- a longer explanation if appropriate.

### Proposal
#### New standard
1. Check that no one else has begun working on the same proposal by checking open branches and/or asking the other devs.
2. Branch off of `main`. Name the branch after the [filepath](#directory-structure) using kebab-case, prefixed with `proposal-` (e.g. `proposal-practices-linting`).
3. Push the empty branch immediately for visibility and to help prevent duplicate efforts.
4. Draft your proposal using the [standard template](../template-standard.md).
5. Create a pull request with a descriptive title.
6. Find another developer to perform the first, cursory review.

#### Amendment
1. Check that no one else has begun working on the same amendment by checking open branches and/or asking the other devs.
2. Branch off of `main`. Name the branch after the [filepath](#directory-structure) using kebab-case, prefixed with `amendment-` (e.g. `amendment-practices-linting`).
3. Push the empty branch immediately for visibility and to help prevent duplicate efforts.
4. Draft your changes.
5. Create a pull request with a descriptive title.
6. Find another developer to perform the first, cursory review.

#### Repeal
1. Check that no one else has begun working on the same repeal by checking open branches and/or asking the other devs.
2. Branch off of `main`. Name the branch after the [filepath](#directory-structure) using kebab-case, prefixed with `repeal-` (e.g. `repeal-practices-linting`).
3. Push the empty branch immediately for visibility and to help prevent duplicate efforts.
4. Draft your changes.
5. Create a pull request with a descriptive title and informative comment.
6. Find another developer to perform the first, cursory review.

### Discussion + refinement
This stage looks a lot like a code review: other devs participate by reading through the proposal, asking questions, and making suggestions. The proposal author makes changes based on feedback. Once ready, the author leaves a comment to indicate voting has begun.

### Vote
Devs vote by using emoji reactions on the initial PR comment **after the author indicates voting started**. 

| Vote    | Emoji  |
|:------- |:------:|
| Yea     | :+1:   |
| Nay     | :-1:   |
| Abstain | :eyes: |

We determine the result with a simple plurality once all devs have voted. Anyone but the author may merge or close the PR once voting ends. Delete the branch after merging.


## Directory structure
This serves merely as an illustrative example. The files may not exist.

```
standards/
|-- frameworks/
|   |-- laravel.md
|   |-- outsystems.md
|   |-- vue.md
|-- languages/
|   |-- css.md
|   |-- html.md
|   |-- javascript.md
|   |-- php.md
|-- practices/
|   |-- automated-testing.md
|   |-- comments.md
|   |-- linting.md
|   |-- pair-and-mob-programming.md
|   |-- peer-review.md
|   |-- qa-testing.md
```
