# rishav
# studio graphene _ technical assignment
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Dynamic Navigation</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <nav class="top-menu" id="topMenu">
        <!-- Navigation items will be added dynamically here -->
    </nav>
    <script src="script.js"></script>
</body>
</html>


/* Add your desired styling for the navigation menu here */
.top-menu {
    background-color: #333;
    color: white;
    display: flex;
    justify-content: space-around;
    align-items: center;
    height: 60px;
    font-size: 18px;
}

.top-menu a {
    text-decoration: none;
    color: white;
}


const navbar = [
    { name: 'Home', id: 'home' },
    { name: 'About', id: 'about' },
    {
        name: 'Our Products', id: 'product', child: [
            { name: 'Product 1', id: 'p1' },
            { name: 'Product 2', id: 'p2' },
            { name: 'Product 3', id: 'p3' },
            { name: 'Product 4', id: 'p4' },
        ]
    },
    { name: 'Contact Us', id: 'contact' },
];

const topMenu = document.getElementById('topMenu');

function createMenuItem(item) {
    const menuItem = document.createElement('a');
    menuItem.textContent = item.name;
    menuItem.href = `#${item.id}`;
    return menuItem;
}

function createSubmenu(submenuItems) {
    const submenu = document.createElement('ul');
    submenuItems.forEach(subItem => {
        const subMenuItem = document.createElement('li');
        subMenuItem.appendChild(createMenuItem(subItem));
        submenu.appendChild(subMenuItem);
    });
    return submenu;
}

navbar.forEach(item => {
    const menuItem = document.createElement('li');
    if (item.child) {
        menuItem.appendChild(createMenuItem(item));
        menuItem.appendChild(createSubmenu(item.child));
    } else {
        menuItem.appendChild(createMenuItem(item));
    }
    topMenu.appendChild(menuItem);
});



<div class="banner">
    Fresh 2022 look
</div>


import React, { useState, useEffect } from 'react';

const Products = () => {
    const [products, setProducts] = useState([]);
    const [filteredProducts, setFilteredProducts] = useState([]);
    const [categoryFilter, setCategoryFilter] = useState('');

    useEffect(() => {
        fetch('https://api.escuelajs.co/api/v1/products')
            .then(response => response.json())
            .then(data => {
                setProducts(data.products);
                setFilteredProducts(data.products);
            });
    }, []);

    useEffect(() => {
        if (categoryFilter) {
            setFilteredProducts(products.filter(product => product.category === categoryFilter));
        } else {
            setFilteredProducts(products);
        }
    }, [categoryFilter, products]);

    return (
        <div>
            <select onChange={e => setCategoryFilter(e.target.value)}>
                <option value="">All</option>
                {/* Add options for categories */}
            </select>
            <div className="product-list">
                {filteredProducts.map(product => (
                    <div key={product.id} className="product">
                        {/* Display product details */}
                    </div>
                ))}
            </div>
        </div>
    );
};

export default Products;



import React, { useState } from 'react';

const ContactForm = () => {
    const [name, setName] = useState('');
    const [email, setEmail] = useState('');
    const [message, setMessage] = useState('');
    const [error, setError] = useState('');

    const handleSubmit = e => {
        e.preventDefault();

        if (!name || !email || !message) {
            setError('All fields are required.');
            return;
        }

        // Perform form submission
    };

    return (
        <form onSubmit={handleSubmit}>
            <input type="text" placeholder="Name" value={name} onChange={e => setName(e.target.value)} />
            <input type="email" placeholder="Email" value={email} onChange={e => setEmail(e.target.value)} />
            <textarea placeholder="Message" value={message} onChange={e => setMessage(e.target.value)} />
            {error && <div className="error">{error}</div>}
            <button type="submit">Submit</button>
        </form>
    );
};

export default ContactForm;

