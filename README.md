# Doom 3 Tokenizer
This project is a Doom 3 text file tokenizer written in Typescript. It is one of the exercises from the book "TypeScript图形渲染实战：2D架构设计与实现".

## Doom3 Text File Format
To implement a tokenizer for a specific file format, we must understand the lexical features of the file, and abstract the classification rules according to the features. Therefore, this section will explain the relevant rules of text files in the Doom3 engine, using the following generic text string:

```typescript
numMeshes 5

/*
 * joints keyword defines skeletal animation's bindPose
 */
joints {
    "origin" -1 (0 0 0) (-0.5 -0.5 -0.5)
    "body" 0 (-12.10381714 0 79.004776001) (-0.5 -0.5 -0.5)
    // origin
}
```

For example, words without double quotes, such as numMeshes and joints, are treated as keywords, that is, some words with specific meanings predefined by the Doom3 engine, which are unique and immutable.

For example, words with double quotation marks such as "origin" and "body" are treated as identifiers. These identifiers are not predefined by the Doom3 engine but are names defined by relevant personnel such as designers or modellers.

The text between "/*" and "*/" is treated as a comment by the tokenizer, and like TypeScript, it means a multi-line comment. The text after the slash "//" is regarded as a single-line comment, which is also consistent with TypeScript's single-line comment.

The brace pair "{ }" represents a block-like module, which can be thought of as a block grouping, similar to TypeScript scopes. Inside the parentheses "( )" is the vector or matrix data represented by floating-point numbers, which can be regarded as an array. It should be noted that the elements of the array are not separated by commas, but separated by space symbols.

There are only two data types in Doom3 text files: strings and numbers, in which keywords and identifiers can be regarded as string types, while numbers can be divided into two types: integers and floating-point numbers.

The above content covers the key points of the Doom3 text file format. Some other hidden rules will be described in the source code of the implementation.
