const fs = require('fs');

// Function to process the input dynamically
function processInput(input) {
    const data = JSON.parse(input);

    const n = data.keys.n;
    const k = data.keys.k;

    const roots = [];
    for (const key in data) {
        if (!isNaN(key)) {
            const base = parseInt(data[key].base);
            const value = parseInt(data[key].value, base);
            roots.push([parseInt(key), value]);
        }
    }

    return { n, k, roots };
}

// Function to compute Lagrange basis polynomial
function basisPolynomial(roots, j, x) {
    let bp = 1;
    const x_j = roots[j][0];
    for (let m = 0; m < roots.length; m++) {
        if (m !== j) {
            const x_m = roots[m][0];
            bp *= (x - x_m) / (x_j - x_m);
        }
    }
    console.log(`Basis Polynomial for j=${j}: ${bp}`);
    return bp;
}

// Lagrange Interpolation function
function lagrangeInterpolation(roots, k) {
    let secret = 0;
    for (let j = 0; j < k; j++) {
        const [x_j, y_j] = roots[j];
        console.log(`Root ${j}: x=${x_j}, y=${y_j}`);
        const bp = basisPolynomial(roots, j, 0);
        console.log(`Lagrange Multiplier for j=${j}: y_j * bp = ${y_j} * ${bp} = ${y_j * bp}`);
        secret += y_j * bp;
    }

    console.log(`Calculated secret before rounding: ${secret}`);
    return Math.round(secret);
}

// Function to handle the dynamic input and find the secret
function findSecretFromInput(input) {
    const { n, k, roots } = processInput(input);
    console.log(`Number of roots provided (n): ${n}`);
    console.log(`Minimum number of roots required (k): ${k}`);
    console.log(`Roots: ${JSON.stringify(roots)}`);

    const secret = lagrangeInterpolation(roots, k);
    return secret;
}

// Sample dynamic input (You can replace this with actual dynamic input)
const sampleInput = `
{
    "keys": {
        "n": 4,
        "k": 3
    },
    "1": {
        "base": "10",
        "value": "4"
    },
    "2": {
        "base": "2",
        "value": "111"
    },
    "3": {
        "base": "10",
        "value": "12"
    },
    "6": {
        "base": "4",
        "value": "213"
    }
}`;

const secret = findSecretFromInput(sampleInput);
console.log(`The secret (c) is: ${secret}`);
