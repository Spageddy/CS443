CREATE TABLE Receipt
(
ReceiptNumber NUMBER,
SalesDate DATE,
CONSTRAINT ReceiptPK PRIMARY KEY(ReceiptNumber)
);

CREATE TABLE Product
(
ProductID NUMBER,
ProductDescription VARCHAR2(200),
CONSTRAINT ProductPK PRIMARY  KEY(ProductID)
);

CREATE TABLE Item
(
ItemNum NUMBER NOT NULL,
ItemDescription VARCHAR2(200),
CONSTRAINT ItemPK PRIMARY KEY(ItemNum)
);

CREATE TABLE Used
(
ItemNum NUMBER,
ProductID NUMBER,
QuantityUsed NUMBER,
CONSTRAINT CheckUsed CHECK(QuantityUsed >=0),
CONSTRAINT UsedPK PRIMARY KEY(ItemNum, ProductID),
CONSTRAINT UsedFK1 FOREIGN KEY(ItemNum) 
	REFERENCES Item(ItemNum),
CONSTRAINT UsedFK2 FOREIGN KEY(ProductID)
	REFERENCES Product(ProductID)
);

CREATE TABLE Sold
(
ReceiptNumber NUMBER,
ProductID NUMBER,
QuantitySold NUMBER
CONSTRAINT CheckSold CHECK(QuantitySold >=0),
CONSTRAINT SoldPK PRIMARY KEY(ReceiptNumber, ProductID),
CONSTRAINT SoldFK1 FOREIGN KEY(ReceiptNumber)
	REFERENCES Receipt(ReceiptNumber),
CONSTRAINT SoldFK2 FOREIGN KEY(ProductID)
	REFERENCES Product(ProductID)
);
