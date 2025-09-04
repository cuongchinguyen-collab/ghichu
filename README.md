notes
hóa đơn loại dơn (xuat tu kho, từ maker về kho, xong từ kho giao KH, giao truc tiep cho khach ) loại dat dơn maker khach hang warehouse đơn giá Đơn OPS ACOS gop don chia don
nouki: ngày giao hàng du kien
nyukabi Ngày hàng về kho
soko: warehouse
shiresaki: supplier
jyu2: Order category
nyu2: Receiving category (Phân loại nhập hang)
den: hóa đơn
tokui: customer
kman: người phụ trách
nyuuka: ngày nhập hàng
okuri: giao hàng
shain: employee
zaiko: hang tồn
daikōten đại lý ủy quyền
shiire Nhập hang
hanbai bán ra
syohin sản phấm
denku phân loại chứng từ
syohin product
bukken: package/item
Jyuki thiết bị gia dụng
Gas 
Buhin phụ tùng (parts)
kensaku tìm kiếm
Ktanka Đơn giá tham khảo
change pass for postgres backup db

SELECT pg_size_pretty(SUM(pg_database_size(datname))) AS total_size

-- count tables in each schema SELECT n.nspname AS schema_name, COUNT(c.relname) AS table_count FROM pg_namespace n LEFT JOIN pg_class c ON n.oid = c.relnamespace WHERE c.relkind = 'r' -- Chỉ lấy các table thông thường AND n.nspname NOT IN ('pg_catalog', 'information_schema') -- Loại bỏ schema hệ thống GROUP BY n.nspname ORDER BY n.nspname;

-- get size of db SELECT pg_database.datname AS database_name, pg_size_pretty(pg_database_size(pg_database.datname)) AS size FROM pg_database WHERE datname = 'tokyo_gas_dev';

-- get size of indexes

SELECT c.relname AS table_name, pg_size_pretty(pg_indexes_size(c.oid)) AS index_size FROM pg_class c JOIN pg_namespace n ON c.relnamespace = n.oid WHERE n.nspname = 'acos2' AND c.relkind = 'r' ORDER BY pg_indexes_size(c.oid) DESC;

Backup: psql "host=192.168.18.22 dbname=postgres user=postgres password=123456 options='-c log_statement=all'" pg_dump -h 160.16.118.79 -U tokyo_gas_dev -d tokyo_gas_dev --no-owner --no-privileges -f tokyo_gas_dev_dump.sql -- pass: Ajd4!0B2
