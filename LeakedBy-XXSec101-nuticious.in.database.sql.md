```bash
-- phpMyAdmin SQL Dump
-- version 4.5.1
-- http://www.phpmyadmin.net
--
-- Host: 127.0.0.1
-- Generation Time: Apr 29, 2016 at 12:04 PM
-- Server version: 10.1.9-MariaDB
-- PHP Version: 5.6.15

SET SQL_MODE = "NO_AUTO_VALUE_ON_ZERO";
SET time_zone = "+00:00";


/*!40101 SET @OLD_CHARACTER_SET_CLIENT=@@CHARACTER_SET_CLIENT */;
/*!40101 SET @OLD_CHARACTER_SET_RESULTS=@@CHARACTER_SET_RESULTS */;
/*!40101 SET @OLD_COLLATION_CONNECTION=@@COLLATION_CONNECTION */;
/*!40101 SET NAMES utf8mb4 */;

--
-- Database: `ves_fasony`
--

-- --------------------------------------------------------

--
-- Table structure for table `adminnotification_inbox`
--

CREATE TABLE `adminnotification_inbox` (
  `notification_id` int(10) UNSIGNED NOT NULL COMMENT 'Notification id',
  `severity` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Problem type',
  `date_added` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT 'Create date',
  `title` varchar(255) NOT NULL COMMENT 'Title',
  `description` text COMMENT 'Description',
  `url` varchar(255) DEFAULT NULL COMMENT 'Url',
  `is_read` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Flag if notification read',
  `is_remove` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Flag if notification might be removed'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Adminnotification Inbox';

-- --------------------------------------------------------

--
-- Table structure for table `admin_passwords`
--

CREATE TABLE `admin_passwords` (
  `password_id` int(10) UNSIGNED NOT NULL COMMENT 'Password Id',
  `user_id` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'User Id',
  `password_hash` varchar(100) DEFAULT NULL COMMENT 'Password Hash',
  `expires` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Expires',
  `last_updated` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Last Updated'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Admin Passwords';

-- --------------------------------------------------------

--
-- Table structure for table `admin_system_messages`
--

CREATE TABLE `admin_system_messages` (
  `identity` varchar(100) NOT NULL COMMENT 'Message id',
  `severity` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Problem type',
  `created_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT 'Create date'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Admin System Messages';

-- --------------------------------------------------------

--
-- Table structure for table `admin_user`
--

CREATE TABLE `admin_user` (
  `user_id` int(10) UNSIGNED NOT NULL COMMENT 'User ID',
  `firstname` varchar(32) DEFAULT NULL COMMENT 'User First Name',
  `lastname` varchar(32) DEFAULT NULL COMMENT 'User Last Name',
  `email` varchar(128) DEFAULT NULL COMMENT 'User Email',
  `username` varchar(40) DEFAULT NULL COMMENT 'User Login',
  `password` varchar(255) NOT NULL COMMENT 'User Password',
  `created` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT 'User Created Time',
  `modified` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP COMMENT 'User Modified Time',
  `logdate` timestamp NULL DEFAULT NULL COMMENT 'User Last Login Time',
  `lognum` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'User Login Number',
  `reload_acl_flag` smallint(6) NOT NULL DEFAULT '0' COMMENT 'Reload ACL',
  `is_active` smallint(6) NOT NULL DEFAULT '1' COMMENT 'User Is Active',
  `extra` text COMMENT 'User Extra Data',
  `rp_token` text COMMENT 'Reset Password Link Token',
  `rp_token_created_at` timestamp NULL DEFAULT NULL COMMENT 'Reset Password Link Token Creation Date',
  `interface_locale` varchar(16) NOT NULL DEFAULT 'en_US' COMMENT 'Backend interface locale',
  `failures_num` smallint(6) DEFAULT '0' COMMENT 'Failure Number',
  `first_failure` timestamp NULL DEFAULT NULL COMMENT 'First Failure',
  `lock_expires` timestamp NULL DEFAULT NULL COMMENT 'Expiration Lock Dates'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Admin User Table';

--
-- Dumping data for table `admin_user`
--

INSERT INTO `admin_user` (`user_id`, `firstname`, `lastname`, `email`, `username`, `password`, `created`, `modified`, `logdate`, `lognum`, `reload_acl_flag`, `is_active`, `extra`, `rp_token`, `rp_token_created_at`, `interface_locale`, `failures_num`, `first_failure`, `lock_expires`) VALUES
(1, 'myadmin', 'myadmin', 'lieult84@gmail.com', 'myadmin', 'a94fbfab0d806677a38752104d4a609e90ffdfd06d1b2e5a69864e673bd1679c:SDWA8eooB4VyonSoUCoP6JukgawHlNYH:1', '2016-04-12 14:17:20', '2016-04-29 09:02:29', '2016-04-29 09:02:29', 42, 0, 1, 'a:1:{s:11:"configState";a:21:{s:12:"design_theme";s:1:"1";s:11:"design_head";s:1:"0";s:27:"design_search_engine_robots";s:1:"0";s:13:"design_header";s:1:"1";s:13:"design_footer";s:1:"1";s:16:"design_watermark";s:1:"0";s:17:"design_pagination";s:1:"0";s:12:"design_email";s:1:"0";s:15:"general_country";s:1:"1";s:14:"general_region";s:1:"0";s:16:"currency_options";s:1:"1";s:25:"trans_email_ident_general";s:1:"1";s:23:"trans_email_ident_sales";s:1:"1";s:25:"trans_email_ident_support";s:1:"1";s:20:"currency_webservicex";s:1:"0";s:15:"currency_import";s:1:"0";s:20:"catalog_fields_masks";s:1:"0";s:14:"catalog_review";s:1:"0";s:16:"catalog_frontend";s:1:"0";s:20:"catalog_downloadable";s:1:"0";s:11:"web_default";s:1:"1";}}', NULL, NULL, 'en_US', 0, NULL, NULL);

-- --------------------------------------------------------

--
-- Table structure for table `authorization_role`
--

CREATE TABLE `authorization_role` (
  `role_id` int(10) UNSIGNED NOT NULL COMMENT 'Role ID',
  `parent_id` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Parent Role ID',
  `tree_level` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Role Tree Level',
  `sort_order` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Role Sort Order',
  `role_type` varchar(1) NOT NULL DEFAULT '0' COMMENT 'Role Type',
  `user_id` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'User ID',
  `user_type` varchar(16) DEFAULT NULL COMMENT 'User Type',
  `role_name` varchar(50) DEFAULT NULL COMMENT 'Role Name'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Admin Role Table';

--
-- Dumping data for table `authorization_role`
--

INSERT INTO `authorization_role` (`role_id`, `parent_id`, `tree_level`, `sort_order`, `role_type`, `user_id`, `user_type`, `role_name`) VALUES
(1, 0, 1, 1, 'G', 0, '2', 'Administrators'),
(2, 1, 2, 0, 'U', 1, '2', 'myadmin');

-- --------------------------------------------------------

--
-- Table structure for table `authorization_rule`
--

CREATE TABLE `authorization_rule` (
  `rule_id` int(10) UNSIGNED NOT NULL COMMENT 'Rule ID',
  `role_id` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Role ID',
  `resource_id` varchar(255) DEFAULT NULL COMMENT 'Resource ID',
  `privileges` varchar(20) DEFAULT NULL COMMENT 'Privileges',
  `permission` varchar(10) DEFAULT NULL COMMENT 'Permission'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Admin Rule Table';

--
-- Dumping data for table `authorization_rule`
--

INSERT INTO `authorization_rule` (`rule_id`, `role_id`, `resource_id`, `privileges`, `permission`) VALUES
(1, 1, 'Magento_Backend::all', NULL, 'allow');

-- --------------------------------------------------------

--
-- Table structure for table `cache`
--

CREATE TABLE `cache` (
  `id` varchar(200) NOT NULL COMMENT 'Cache Id',
  `data` mediumblob COMMENT 'Cache Data',
  `create_time` int(11) DEFAULT NULL COMMENT 'Cache Creation Time',
  `update_time` int(11) DEFAULT NULL COMMENT 'Time of Cache Updating',
  `expire_time` int(11) DEFAULT NULL COMMENT 'Cache Expiration Time'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Caches';

-- --------------------------------------------------------

--
-- Table structure for table `cache_tag`
--

CREATE TABLE `cache_tag` (
  `tag` varchar(100) NOT NULL COMMENT 'Tag',
  `cache_id` varchar(200) NOT NULL COMMENT 'Cache Id'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Tag Caches';

-- --------------------------------------------------------

--
-- Table structure for table `captcha_log`
--

CREATE TABLE `captcha_log` (
  `type` varchar(32) NOT NULL COMMENT 'Type',
  `value` varchar(32) NOT NULL COMMENT 'Value',
  `count` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Count',
  `updated_at` timestamp NULL DEFAULT NULL COMMENT 'Update Time'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Count Login Attempts';

-- --------------------------------------------------------

--
-- Table structure for table `cataloginventory_stock`
--

CREATE TABLE `cataloginventory_stock` (
  `stock_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Stock Id',
  `website_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Website Id',
  `stock_name` varchar(255) DEFAULT NULL COMMENT 'Stock Name'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Cataloginventory Stock';

--
-- Dumping data for table `cataloginventory_stock`
--

INSERT INTO `cataloginventory_stock` (`stock_id`, `website_id`, `stock_name`) VALUES
(1, 0, 'Default');

-- --------------------------------------------------------

--
-- Table structure for table `cataloginventory_stock_item`
--

CREATE TABLE `cataloginventory_stock_item` (
  `item_id` int(10) UNSIGNED NOT NULL COMMENT 'Item Id',
  `product_id` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Product Id',
  `stock_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Stock Id',
  `qty` decimal(12,4) DEFAULT NULL COMMENT 'Qty',
  `min_qty` decimal(12,4) NOT NULL DEFAULT '0.0000' COMMENT 'Min Qty',
  `use_config_min_qty` smallint(5) UNSIGNED NOT NULL DEFAULT '1' COMMENT 'Use Config Min Qty',
  `is_qty_decimal` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Is Qty Decimal',
  `backorders` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Backorders',
  `use_config_backorders` smallint(5) UNSIGNED NOT NULL DEFAULT '1' COMMENT 'Use Config Backorders',
  `min_sale_qty` decimal(12,4) NOT NULL DEFAULT '1.0000' COMMENT 'Min Sale Qty',
  `use_config_min_sale_qty` smallint(5) UNSIGNED NOT NULL DEFAULT '1' COMMENT 'Use Config Min Sale Qty',
  `max_sale_qty` decimal(12,4) NOT NULL DEFAULT '0.0000' COMMENT 'Max Sale Qty',
  `use_config_max_sale_qty` smallint(5) UNSIGNED NOT NULL DEFAULT '1' COMMENT 'Use Config Max Sale Qty',
  `is_in_stock` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Is In Stock',
  `low_stock_date` timestamp NULL DEFAULT NULL COMMENT 'Low Stock Date',
  `notify_stock_qty` decimal(12,4) DEFAULT NULL COMMENT 'Notify Stock Qty',
  `use_config_notify_stock_qty` smallint(5) UNSIGNED NOT NULL DEFAULT '1' COMMENT 'Use Config Notify Stock Qty',
  `manage_stock` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Manage Stock',
  `use_config_manage_stock` smallint(5) UNSIGNED NOT NULL DEFAULT '1' COMMENT 'Use Config Manage Stock',
  `stock_status_changed_auto` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Stock Status Changed Automatically',
  `use_config_qty_increments` smallint(5) UNSIGNED NOT NULL DEFAULT '1' COMMENT 'Use Config Qty Increments',
  `qty_increments` decimal(12,4) NOT NULL DEFAULT '0.0000' COMMENT 'Qty Increments',
  `use_config_enable_qty_inc` smallint(5) UNSIGNED NOT NULL DEFAULT '1' COMMENT 'Use Config Enable Qty Increments',
  `enable_qty_increments` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Enable Qty Increments',
  `is_decimal_divided` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Is Divided into Multiple Boxes for Shipping',
  `website_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Is Divided into Multiple Boxes for Shipping'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Cataloginventory Stock Item';

--
-- Dumping data for table `cataloginventory_stock_item`
--

INSERT INTO `cataloginventory_stock_item` (`item_id`, `product_id`, `stock_id`, `qty`, `min_qty`, `use_config_min_qty`, `is_qty_decimal`, `backorders`, `use_config_backorders`, `min_sale_qty`, `use_config_min_sale_qty`, `max_sale_qty`, `use_config_max_sale_qty`, `is_in_stock`, `low_stock_date`, `notify_stock_qty`, `use_config_notify_stock_qty`, `manage_stock`, `use_config_manage_stock`, `stock_status_changed_auto`, `use_config_qty_increments`, `qty_increments`, `use_config_enable_qty_inc`, `enable_qty_increments`, `is_decimal_divided`, `website_id`) VALUES
(1, 1, 1, '950.0000', '0.0000', 1, 0, 0, 1, '1.0000', 1, '10000.0000', 1, 1, NULL, '1.0000', 1, 1, 0, 0, 1, '0.0000', 0, 0, 0, 1),
(2, 2, 1, '500.0000', '0.0000', 1, 0, 0, 1, '1.0000', 1, '10000.0000', 1, 1, NULL, '1.0000', 1, 1, 1, 0, 1, '0.0000', 0, 0, 0, 1),
(3, 3, 1, '498.0000', '0.0000', 1, 0, 0, 1, '1.0000', 1, '10000.0000', 1, 1, NULL, '1.0000', 1, 1, 1, 0, 1, '0.0000', 0, 0, 0, 1),
(4, 4, 1, '498.0000', '0.0000', 1, 0, 0, 1, '1.0000', 1, '10000.0000', 1, 1, NULL, '1.0000', 1, 1, 1, 0, 1, '0.0000', 0, 0, 0, 1),
(5, 5, 1, '0.0000', '0.0000', 1, 0, 0, 1, '1.0000', 1, '10000.0000', 1, 1, NULL, '1.0000', 1, 0, 0, 1, 1, '0.0000', 0, 0, 0, 1),
(6, 6, 1, NULL, '0.0000', 1, 0, 0, 1, '1.0000', 1, '10000.0000', 1, 0, '2016-04-19 07:24:23', '1.0000', 1, 0, 0, 0, 1, '0.0000', 0, 0, 0, 1),
(7, 7, 1, NULL, '0.0000', 1, 0, 0, 1, '1.0000', 1, '10000.0000', 1, 0, '2016-04-19 07:24:24', '1.0000', 1, 0, 0, 0, 1, '0.0000', 0, 0, 0, 1),
(8, 8, 1, NULL, '0.0000', 1, 0, 0, 1, '1.0000', 1, '10000.0000', 1, 0, '2016-04-19 07:24:25', '1.0000', 1, 0, 0, 0, 1, '0.0000', 0, 0, 0, 1),
(9, 9, 1, '0.0000', '0.0000', 1, 0, 0, 1, '1.0000', 1, '0.0000', 1, 1, NULL, NULL, 1, 1, 1, 0, 1, '0.0000', 0, 0, 0, 1),
(10, 10, 1, '0.0000', '0.0000', 1, 0, 0, 1, '1.0000', 1, '0.0000', 1, 1, NULL, NULL, 1, 1, 1, 0, 1, '0.0000', 0, 0, 0, 1),
(11, 12, 1, '500.0000', '0.0000', 1, 0, 0, 1, '1.0000', 1, '10000.0000', 1, 1, NULL, '1.0000', 1, 1, 1, 0, 1, '0.0000', 0, 0, 0, 1);

-- --------------------------------------------------------

--
-- Table structure for table `cataloginventory_stock_status`
--

CREATE TABLE `cataloginventory_stock_status` (
  `product_id` int(10) UNSIGNED NOT NULL COMMENT 'Product Id',
  `website_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Website Id',
  `stock_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Stock Id',
  `qty` decimal(12,4) NOT NULL DEFAULT '0.0000' COMMENT 'Qty',
  `stock_status` smallint(5) UNSIGNED NOT NULL COMMENT 'Stock Status'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Cataloginventory Stock Status';

--
-- Dumping data for table `cataloginventory_stock_status`
--

INSERT INTO `cataloginventory_stock_status` (`product_id`, `website_id`, `stock_id`, `qty`, `stock_status`) VALUES
(1, 1, 1, '950.0000', 1),
(2, 1, 1, '500.0000', 1),
(3, 1, 1, '498.0000', 1),
(4, 1, 1, '498.0000', 1),
(5, 1, 1, '0.0000', 1),
(6, 1, 1, '0.0000', 1),
(7, 1, 1, '0.0000', 1),
(8, 1, 1, '0.0000', 1),
(9, 1, 1, '0.0000', 1),
(10, 1, 1, '0.0000', 1),
(12, 1, 1, '500.0000', 1);

-- --------------------------------------------------------

--
-- Table structure for table `cataloginventory_stock_status_idx`
--

CREATE TABLE `cataloginventory_stock_status_idx` (
  `product_id` int(10) UNSIGNED NOT NULL COMMENT 'Product Id',
  `website_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Website Id',
  `stock_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Stock Id',
  `qty` decimal(12,4) NOT NULL DEFAULT '0.0000' COMMENT 'Qty',
  `stock_status` smallint(5) UNSIGNED NOT NULL COMMENT 'Stock Status'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Cataloginventory Stock Status Indexer Idx';

--
-- Dumping data for table `cataloginventory_stock_status_idx`
--

INSERT INTO `cataloginventory_stock_status_idx` (`product_id`, `website_id`, `stock_id`, `qty`, `stock_status`) VALUES
(1, 1, 1, '950.0000', 1),
(2, 1, 1, '500.0000', 1),
(3, 1, 1, '498.0000', 1),
(4, 1, 1, '498.0000', 1),
(5, 1, 1, '0.0000', 1),
(6, 1, 1, '0.0000', 1),
(7, 1, 1, '0.0000', 1),
(8, 1, 1, '0.0000', 1),
(9, 1, 1, '0.0000', 1),
(10, 1, 1, '0.0000', 1),
(12, 1, 1, '500.0000', 1);

-- --------------------------------------------------------

--
-- Table structure for table `cataloginventory_stock_status_tmp`
--

CREATE TABLE `cataloginventory_stock_status_tmp` (
  `product_id` int(10) UNSIGNED NOT NULL COMMENT 'Product Id',
  `website_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Website Id',
  `stock_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Stock Id',
  `qty` decimal(12,4) NOT NULL DEFAULT '0.0000' COMMENT 'Qty',
  `stock_status` smallint(5) UNSIGNED NOT NULL COMMENT 'Stock Status'
) ENGINE=MEMORY DEFAULT CHARSET=utf8 COMMENT='Cataloginventory Stock Status Indexer Tmp';

-- --------------------------------------------------------

--
-- Table structure for table `catalogrule`
--

CREATE TABLE `catalogrule` (
  `rule_id` int(10) UNSIGNED NOT NULL COMMENT 'Rule Id',
  `name` varchar(255) DEFAULT NULL COMMENT 'Name',
  `description` text COMMENT 'Description',
  `from_date` date DEFAULT NULL COMMENT 'From',
  `to_date` date DEFAULT NULL COMMENT 'To',
  `is_active` smallint(6) NOT NULL DEFAULT '0' COMMENT 'Is Active',
  `conditions_serialized` mediumtext COMMENT 'Conditions Serialized',
  `actions_serialized` mediumtext COMMENT 'Actions Serialized',
  `stop_rules_processing` smallint(6) NOT NULL DEFAULT '1' COMMENT 'Stop Rules Processing',
  `sort_order` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Sort Order',
  `simple_action` varchar(32) DEFAULT NULL COMMENT 'Simple Action',
  `discount_amount` decimal(12,4) NOT NULL DEFAULT '0.0000' COMMENT 'Discount Amount',
  `sub_is_enable` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Is Rule Enable For Subitems',
  `sub_simple_action` varchar(32) DEFAULT NULL COMMENT 'Simple Action For Subitems',
  `sub_discount_amount` decimal(12,4) NOT NULL DEFAULT '0.0000' COMMENT 'Discount Amount For Subitems'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='CatalogRule';

-- --------------------------------------------------------

--
-- Table structure for table `catalogrule_customer_group`
--

CREATE TABLE `catalogrule_customer_group` (
  `rule_id` int(10) UNSIGNED NOT NULL COMMENT 'Rule Id',
  `customer_group_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Customer Group Id'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Catalog Rules To Customer Groups Relations';

-- --------------------------------------------------------

--
-- Table structure for table `catalogrule_group_website`
--

CREATE TABLE `catalogrule_group_website` (
  `rule_id` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Rule Id',
  `customer_group_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Customer Group Id',
  `website_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Website Id'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='CatalogRule Group Website';

-- --------------------------------------------------------

--
-- Table structure for table `catalogrule_product`
--

CREATE TABLE `catalogrule_product` (
  `rule_product_id` int(10) UNSIGNED NOT NULL COMMENT 'Rule Product Id',
  `rule_id` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Rule Id',
  `from_time` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'From Time',
  `to_time` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'To time',
  `customer_group_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Customer Group Id',
  `product_id` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Product Id',
  `action_operator` varchar(10) DEFAULT 'to_fixed' COMMENT 'Action Operator',
  `action_amount` decimal(12,4) NOT NULL DEFAULT '0.0000' COMMENT 'Action Amount',
  `action_stop` smallint(6) NOT NULL DEFAULT '0' COMMENT 'Action Stop',
  `sort_order` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Sort Order',
  `website_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Website Id',
  `sub_simple_action` varchar(32) DEFAULT NULL COMMENT 'Simple Action For Subitems',
  `sub_discount_amount` decimal(12,4) NOT NULL DEFAULT '0.0000' COMMENT 'Discount Amount For Subitems'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='CatalogRule Product';

-- --------------------------------------------------------

--
-- Table structure for table `catalogrule_product_price`
--

CREATE TABLE `catalogrule_product_price` (
  `rule_product_price_id` int(10) UNSIGNED NOT NULL COMMENT 'Rule Product PriceId',
  `rule_date` date NOT NULL COMMENT 'Rule Date',
  `customer_group_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Customer Group Id',
  `product_id` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Product Id',
  `rule_price` decimal(12,4) NOT NULL DEFAULT '0.0000' COMMENT 'Rule Price',
  `website_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Website Id',
  `latest_start_date` date DEFAULT NULL COMMENT 'Latest StartDate',
  `earliest_end_date` date DEFAULT NULL COMMENT 'Earliest EndDate'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='CatalogRule Product Price';

-- --------------------------------------------------------

--
-- Table structure for table `catalogrule_website`
--

CREATE TABLE `catalogrule_website` (
  `rule_id` int(10) UNSIGNED NOT NULL COMMENT 'Rule Id',
  `website_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Website Id'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Catalog Rules To Websites Relations';

-- --------------------------------------------------------

--
-- Table structure for table `catalogsearch_fulltext_scope1`
--

CREATE TABLE `catalogsearch_fulltext_scope1` (
  `entity_id` int(10) UNSIGNED NOT NULL COMMENT 'Entity ID',
  `attribute_id` int(10) UNSIGNED NOT NULL COMMENT 'Attribute_id',
  `data_index` longtext COMMENT 'Data index'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='catalogsearch_fulltext_scope1';

--
-- Dumping data for table `catalogsearch_fulltext_scope1`
--

INSERT INTO `catalogsearch_fulltext_scope1` (`entity_id`, `attribute_id`, `data_index`) VALUES
(1, 70, 'Ariel Roll Sleeve Sweatshirt'),
(1, 71, 'Ariel Roll Sleeve Sweatshirt'),
(1, 72, 'Soft, sleek and subtle, the Ariel Roll Sleeve Sweatshirt is a nuanced fitness garment for all occasions. It works equally well as a workout piece or in a casual social setting. &bull; Purple two-tone lightweight hoodie. &bull; 100% cotton.&bull; Adjustable roll sleeves for Long-Sleeve or 3/4 sleeve.&bull; Casual, comfy piece for running errands or weekend activities.'),
(1, 73, 'You won''t know what you like best about the Antonia Racer Tank: soft, stretchy, lightweight fabric? Super-cute colorblocked details? Whatever it is, this piece is sure to quickly move to the top of your workout rotation.'),
(2, 70, 'Arcadio Gym Short-32-Blue'),
(2, 71, 'Arcadio Gym Short-32-Blue'),
(2, 72, 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed aliquam magna consequat fringilla consectetur. Duis ut elit sed nunc auctor malesuada et ac mi. Donec non diam a lectus hendrerit aliquet sed ut orci. Suspendisse et facilisis nunc. Fusce dolor eros, suscipit sit amet varius et, iaculis vitae leo. Donec sit amet venenatis massa. Pellentesque consequat laoreet urna sollicitudin volutpat. Integer congue felis a quam pulvinar tristique. Class aptent taciti sociosqu ad litora torquent per conubia nostra, per inceptos himenaeos. Donec fringilla pharetra justo ac tristique. Phasellus pulvinar orci a lorem eleifend, scelerisque ullamcorper purus suscipit.'),
(2, 73, 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed aliquam magna consequat fringilla consectetur. Duis ut elit sed nunc auctor malesuada et ac mi. Donec non diam a lectus hendrerit aliquet sed ut orci. Suspendisse et facilisis nunc. Fusce dolor eros, suscipit sit amet varius et, iaculis vitae leo. Donec sit amet venenatis massa. Pellentesque consequat laoreet urna sollicitudin volutpat. Integer congue felis a quam pulvinar tristique. Class aptent taciti sociosqu ad litora torquent per conubia nostra, per inceptos himenaeos. Donec fringilla pharetra justo ac tristique. Phasellus pulvinar orci a lorem eleifend, scelerisque ullamcorper purus suscipit.'),
(3, 70, 'Atomic Endurance Running Tee'),
(3, 71, 'Atomic Endurance Running Tee'),
(3, 72, 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed aliquam magna consequat fringilla consectetur. Duis ut elit sed nunc auctor malesuada et ac mi. Donec non diam a lectus hendrerit aliquet sed ut orci. Suspendisse et facilisis nunc. Fusce dolor eros, suscipit sit amet varius et, iaculis vitae leo. Donec sit amet venenatis massa. Pellentesque consequat laoreet urna sollicitudin volutpat. Integer congue felis a quam pulvinar tristique. Class aptent taciti sociosqu ad litora torquent per conubia nostra, per inceptos himenaeos. Donec fringilla pharetra justo ac tristique. Phasellus pulvinar orci a lorem eleifend, scelerisque ullamcorper purus suscipit.'),
(3, 73, 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed aliquam magna consequat fringilla consectetur. Duis ut elit sed nunc auctor malesuada et ac mi. Donec non diam a lectus hendrerit aliquet sed ut orci. Suspendisse et facilisis nunc. Fusce dolor eros, suscipit sit amet varius et, iaculis vitae leo. Donec sit amet venenatis massa. Pellentesque consequat laoreet urna sollicitudin volutpat. Integer congue felis a quam pulvinar tristique. Class aptent taciti sociosqu ad litora torquent per conubia nostra, per inceptos himenaeos. Donec fringilla pharetra justo ac tristique. Phasellus pulvinar orci a lorem eleifend, scelerisque ullamcorper purus suscipit.'),
(4, 70, 'Arcadio Gym Short'),
(4, 71, 'Arcadio Gym Short'),
(4, 72, 'You won''t know what you like best about the Antonia Racer Tank: soft, stretchy, lightweight fabric? Super-cute colorblocked details? Whatever it is, this piece is sure to quickly move to the top of your workout rotation.'),
(4, 73, 'You won''t know what you like best about the Antonia Racer Tank: soft, stretchy, lightweight fabric? Super-cute colorblocked details? Whatever it is, this piece is sure to quickly move to the top of your workout rotation.'),
(5, 70, 'product configuration magento | product configuration magento-blue | product configuration magento-pink | product configuration magento-red'),
(5, 71, 'product configuration magento'),
(5, 72, 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed aliquam magna consequat fringilla consectetur. Duis ut elit sed nunc auctor malesuada et ac mi. Donec non diam a lectus hendrerit aliquet sed ut orci. Suspendisse et facilisis nunc. Fusce dolor eros, suscipit sit amet varius et, iaculis vitae leo. Donec sit amet venenatis massa. Pellentesque consequat laoreet urna sollicitudin volutpat. Integer congue felis a quam pulvinar tristique. Class aptent taciti sociosqu ad litora torquent per conubia nostra, per inceptos himenaeos. Donec fringilla pharetra justo ac tristique. Phasellus pulvinar orci a lorem eleifend, scelerisque ullamcorper purus suscipit.'),
(5, 73, 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed aliquam magna consequat fringilla consectetur. Duis ut elit sed nunc auctor malesuada et ac mi. Donec non diam a lectus hendrerit aliquet sed ut orci. Suspendisse et facilisis nunc. Fusce dolor eros, suscipit sit amet varius et, iaculis vitae leo. Donec sit amet venenatis massa. Pellentesque consequat laoreet urna sollicitudin volutpat. Integer congue felis a quam pulvinar tristique. Class aptent taciti sociosqu ad litora torquent per conubia nostra, per inceptos himenaeos. Donec fringilla pharetra justo ac tristique. Phasellus pulvinar orci a lorem eleifend, scelerisque ullamcorper purus suscipit.'),
(5, 90, 'blue | pink | red'),
(9, 0, 'Custom option name'),
(9, 70, 'Magento Bundle Product Type | Ariel Roll Sleeve Sweatshirt | product configuration magento-blue'),
(9, 71, 'Magento Bundle Product Type'),
(9, 72, 'You won''t know what you like best about the Antonia Racer Tank: soft, stretchy, lightweight fabric? Super-cute colorblocked details? Whatever it is, this piece is sure to quickly move to the top of your workout rotation. You won''t know what you like best about the Antonia Racer Tank: soft, stretchy, lightweight fabric? Super-cute colorblocked details? Whatever it is, this piece is sure to quickly move to the top of your workout rotation. You won''t know what you like best about the Antonia Racer Tank: soft, stretchy, lightweight fabric? Super-cute colorblocked details? Whatever it is, this piece is sure to quickly move to the top of your workout rotation. | Soft, sleek and subtle, the Ariel Roll Sleeve Sweatshirt is a nuanced fitness garment for all occasions. It works equally well as a workout piece or in a casual social setting. &bull; Purple two-tone lightweight hoodie. &bull; 100% cotton.&bull; Adjustable roll sleeves for Long-Sleeve or 3/4 sleeve.&bull; Casual, comfy piece for running errands or weekend activities.'),
(9, 73, 'You won''t know what you like best about the Antonia Racer Tank: soft, stretchy, lightweight fabric? Super-cute colorblocked details? Whatever it is, this piece is sure to quickly move to the top of your workout rotation. | You won''t know what you like best about the Antonia Racer Tank: soft, stretchy, lightweight fabric? Super-cute colorblocked details? Whatever it is, this piece is sure to quickly move to the top of your workout rotation.'),
(9, 90, 'blue'),
(10, 70, 'Magento grouped products type | Atomic Endurance Running Tee | Arcadio Gym Short'),
(10, 71, 'Grouped products'),
(10, 72, 'You won''t know what you like best about the Antonia Racer Tank: soft, stretchy, lightweight fabric? Super-cute colorblocked details? Whatever it is, this piece is sure to quickly move to the top of your workout rotation. You won''t know what you like best about the Antonia Racer Tank: soft, stretchy, lightweight fabric? Super-cute colorblocked details? Whatever it is, this piece is sure to quickly move to the top of your workout rotation. You won''t know what you like best about the Antonia Racer Tank: soft, stretchy, lightweight fabric? Super-cute colorblocked details? Whatever it is, this piece is sure to quickly move to the top of your workout rotation. | Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed aliquam magna consequat fringilla consectetur. Duis ut elit sed nunc auctor malesuada et ac mi. Donec non diam a lectus hendrerit aliquet sed ut orci. Suspendisse et facilisis nunc. Fusce dolor eros, suscipit sit amet varius et, iaculis vitae leo. Donec sit amet venenatis massa. Pellentesque consequat laoreet urna sollicitudin volutpat. Integer congue felis a quam pulvinar tristique. Class aptent taciti sociosqu ad litora torquent per conubia nostra, per inceptos himenaeos. Donec fringilla pharetra justo ac tristique. Phasellus pulvinar orci a lorem eleifend, scelerisque ullamcorper purus suscipit. | You won''t know what you like best about the Antonia Racer Tank: soft, stretchy, lightweight fabric? Super-cute colorblocked details? Whatever it is, this piece is sure to quickly move to the top of your workout rotation.'),
(10, 73, 'You won''t know what you like best about the Antonia Racer Tank: soft, stretchy, lightweight fabric? Super-cute colorblocked details? Whatever it is, this piece is sure to quickly move to the top of your workout rotation. | Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed aliquam magna consequat fringilla consectetur. Duis ut elit sed nunc auctor malesuada et ac mi. Donec non diam a lectus hendrerit aliquet sed ut orci. Suspendisse et facilisis nunc. Fusce dolor eros, suscipit sit amet varius et, iaculis vitae leo. Donec sit amet venenatis massa. Pellentesque consequat laoreet urna sollicitudin volutpat. Integer congue felis a quam pulvinar tristique. Class aptent taciti sociosqu ad litora torquent per conubia nostra, per inceptos himenaeos. Donec fringilla pharetra justo ac tristique. Phasellus pulvinar orci a lorem eleifend, scelerisque ullamcorper purus suscipit. | You won''t know what you like best about the Antonia Racer Tank: soft, stretchy, lightweight fabric? Super-cute colorblocked details? Whatever it is, this piece is sure to quickly move to the top of your workout rotation.'),
(12, 70, 'Ariel Roll Sleeve Sweatshirt women'),
(12, 71, 'Ariel Roll Sleeve Sweatshirt women'),
(12, 72, 'You won''t know what you like best about the Antonia Racer Tank: soft, stretchy, lightweight fabric? Super-cute colorblocked details? Whatever it is, this piece is sure to quickly move to the top of your workout rotation. You won''t know what you like best about the Antonia Racer Tank: soft, stretchy, lightweight fabric? Super-cute colorblocked details? Whatever it is, this piece is sure to quickly move to the top of your workout rotation. You won''t know what you like best about the Antonia Racer Tank: soft, stretchy, lightweight fabric? Super-cute colorblocked details? Whatever it is, this piece is sure to quickly move to the top of your workout rotation.'),
(12, 73, 'You won''t know what you like best about the Antonia Racer Tank: soft, stretchy, lightweight fabric? Super-cute colorblocked details? Whatever it is, this piece is sure to quickly move to the top of your workout rotation.'),
(12, 90, 'blue');

-- --------------------------------------------------------

--
-- Table structure for table `catalogsearch_fulltext_scope2`
--

CREATE TABLE `catalogsearch_fulltext_scope2` (
  `entity_id` int(10) UNSIGNED NOT NULL COMMENT 'Entity ID',
  `attribute_id` int(10) UNSIGNED NOT NULL COMMENT 'Attribute_id',
  `data_index` longtext COMMENT 'Data index'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='catalogsearch_fulltext_scope2';

--
-- Dumping data for table `catalogsearch_fulltext_scope2`
--

INSERT INTO `catalogsearch_fulltext_scope2` (`entity_id`, `attribute_id`, `data_index`) VALUES
(1, 70, 'Ariel Roll Sleeve Sweatshirt'),
(1, 71, 'Ariel Roll Sleeve Sweatshirt'),
(1, 72, 'Soft, sleek and subtle, the Ariel Roll Sleeve Sweatshirt is a nuanced fitness garment for all occasions. It works equally well as a workout piece or in a casual social setting. &bull; Purple two-tone lightweight hoodie. &bull; 100% cotton.&bull; Adjustable roll sleeves for Long-Sleeve or 3/4 sleeve.&bull; Casual, comfy piece for running errands or weekend activities.'),
(1, 73, 'You won''t know what you like best about the Antonia Racer Tank: soft, stretchy, lightweight fabric? Super-cute colorblocked details? Whatever it is, this piece is sure to quickly move to the top of your workout rotation.'),
(2, 70, 'Arcadio Gym Short-32-Blue'),
(2, 71, 'Arcadio Gym Short-32-Blue'),
(2, 72, 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed aliquam magna consequat fringilla consectetur. Duis ut elit sed nunc auctor malesuada et ac mi. Donec non diam a lectus hendrerit aliquet sed ut orci. Suspendisse et facilisis nunc. Fusce dolor eros, suscipit sit amet varius et, iaculis vitae leo. Donec sit amet venenatis massa. Pellentesque consequat laoreet urna sollicitudin volutpat. Integer congue felis a quam pulvinar tristique. Class aptent taciti sociosqu ad litora torquent per conubia nostra, per inceptos himenaeos. Donec fringilla pharetra justo ac tristique. Phasellus pulvinar orci a lorem eleifend, scelerisque ullamcorper purus suscipit.'),
(2, 73, 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed aliquam magna consequat fringilla consectetur. Duis ut elit sed nunc auctor malesuada et ac mi. Donec non diam a lectus hendrerit aliquet sed ut orci. Suspendisse et facilisis nunc. Fusce dolor eros, suscipit sit amet varius et, iaculis vitae leo. Donec sit amet venenatis massa. Pellentesque consequat laoreet urna sollicitudin volutpat. Integer congue felis a quam pulvinar tristique. Class aptent taciti sociosqu ad litora torquent per conubia nostra, per inceptos himenaeos. Donec fringilla pharetra justo ac tristique. Phasellus pulvinar orci a lorem eleifend, scelerisque ullamcorper purus suscipit.'),
(3, 70, 'Atomic Endurance Running Tee'),
(3, 71, 'Atomic Endurance Running Tee'),
(3, 72, 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed aliquam magna consequat fringilla consectetur. Duis ut elit sed nunc auctor malesuada et ac mi. Donec non diam a lectus hendrerit aliquet sed ut orci. Suspendisse et facilisis nunc. Fusce dolor eros, suscipit sit amet varius et, iaculis vitae leo. Donec sit amet venenatis massa. Pellentesque consequat laoreet urna sollicitudin volutpat. Integer congue felis a quam pulvinar tristique. Class aptent taciti sociosqu ad litora torquent per conubia nostra, per inceptos himenaeos. Donec fringilla pharetra justo ac tristique. Phasellus pulvinar orci a lorem eleifend, scelerisque ullamcorper purus suscipit.'),
(3, 73, 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed aliquam magna consequat fringilla consectetur. Duis ut elit sed nunc auctor malesuada et ac mi. Donec non diam a lectus hendrerit aliquet sed ut orci. Suspendisse et facilisis nunc. Fusce dolor eros, suscipit sit amet varius et, iaculis vitae leo. Donec sit amet venenatis massa. Pellentesque consequat laoreet urna sollicitudin volutpat. Integer congue felis a quam pulvinar tristique. Class aptent taciti sociosqu ad litora torquent per conubia nostra, per inceptos himenaeos. Donec fringilla pharetra justo ac tristique. Phasellus pulvinar orci a lorem eleifend, scelerisque ullamcorper purus suscipit.'),
(4, 70, 'Arcadio Gym Short'),
(4, 71, 'Arcadio Gym Short'),
(4, 72, 'You won''t know what you like best about the Antonia Racer Tank: soft, stretchy, lightweight fabric? Super-cute colorblocked details? Whatever it is, this piece is sure to quickly move to the top of your workout rotation.'),
(4, 73, 'You won''t know what you like best about the Antonia Racer Tank: soft, stretchy, lightweight fabric? Super-cute colorblocked details? Whatever it is, this piece is sure to quickly move to the top of your workout rotation.'),
(5, 70, 'product configuration magento | product configuration magento-blue | product configuration magento-pink | product configuration magento-red'),
(5, 71, 'product configuration magento'),
(5, 72, 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed aliquam magna consequat fringilla consectetur. Duis ut elit sed nunc auctor malesuada et ac mi. Donec non diam a lectus hendrerit aliquet sed ut orci. Suspendisse et facilisis nunc. Fusce dolor eros, suscipit sit amet varius et, iaculis vitae leo. Donec sit amet venenatis massa. Pellentesque consequat laoreet urna sollicitudin volutpat. Integer congue felis a quam pulvinar tristique. Class aptent taciti sociosqu ad litora torquent per conubia nostra, per inceptos himenaeos. Donec fringilla pharetra justo ac tristique. Phasellus pulvinar orci a lorem eleifend, scelerisque ullamcorper purus suscipit.'),
(5, 73, 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed aliquam magna consequat fringilla consectetur. Duis ut elit sed nunc auctor malesuada et ac mi. Donec non diam a lectus hendrerit aliquet sed ut orci. Suspendisse et facilisis nunc. Fusce dolor eros, suscipit sit amet varius et, iaculis vitae leo. Donec sit amet venenatis massa. Pellentesque consequat laoreet urna sollicitudin volutpat. Integer congue felis a quam pulvinar tristique. Class aptent taciti sociosqu ad litora torquent per conubia nostra, per inceptos himenaeos. Donec fringilla pharetra justo ac tristique. Phasellus pulvinar orci a lorem eleifend, scelerisque ullamcorper purus suscipit.'),
(5, 90, 'blue | pink | red'),
(9, 0, 'Custom option name'),
(9, 70, 'Magento Bundle Product Type | Ariel Roll Sleeve Sweatshirt | product configuration magento-blue'),
(9, 71, 'Magento Bundle Product Type'),
(9, 72, 'You won''t know what you like best about the Antonia Racer Tank: soft, stretchy, lightweight fabric? Super-cute colorblocked details? Whatever it is, this piece is sure to quickly move to the top of your workout rotation. You won''t know what you like best about the Antonia Racer Tank: soft, stretchy, lightweight fabric? Super-cute colorblocked details? Whatever it is, this piece is sure to quickly move to the top of your workout rotation. You won''t know what you like best about the Antonia Racer Tank: soft, stretchy, lightweight fabric? Super-cute colorblocked details? Whatever it is, this piece is sure to quickly move to the top of your workout rotation. | Soft, sleek and subtle, the Ariel Roll Sleeve Sweatshirt is a nuanced fitness garment for all occasions. It works equally well as a workout piece or in a casual social setting. &bull; Purple two-tone lightweight hoodie. &bull; 100% cotton.&bull; Adjustable roll sleeves for Long-Sleeve or 3/4 sleeve.&bull; Casual, comfy piece for running errands or weekend activities.'),
(9, 73, 'You won''t know what you like best about the Antonia Racer Tank: soft, stretchy, lightweight fabric? Super-cute colorblocked details? Whatever it is, this piece is sure to quickly move to the top of your workout rotation. | You won''t know what you like best about the Antonia Racer Tank: soft, stretchy, lightweight fabric? Super-cute colorblocked details? Whatever it is, this piece is sure to quickly move to the top of your workout rotation.'),
(9, 90, 'blue'),
(10, 70, 'Magento grouped products type | Atomic Endurance Running Tee | Arcadio Gym Short'),
(10, 71, 'Grouped products'),
(10, 72, 'You won''t know what you like best about the Antonia Racer Tank: soft, stretchy, lightweight fabric? Super-cute colorblocked details? Whatever it is, this piece is sure to quickly move to the top of your workout rotation. You won''t know what you like best about the Antonia Racer Tank: soft, stretchy, lightweight fabric? Super-cute colorblocked details? Whatever it is, this piece is sure to quickly move to the top of your workout rotation. You won''t know what you like best about the Antonia Racer Tank: soft, stretchy, lightweight fabric? Super-cute colorblocked details? Whatever it is, this piece is sure to quickly move to the top of your workout rotation. | Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed aliquam magna consequat fringilla consectetur. Duis ut elit sed nunc auctor malesuada et ac mi. Donec non diam a lectus hendrerit aliquet sed ut orci. Suspendisse et facilisis nunc. Fusce dolor eros, suscipit sit amet varius et, iaculis vitae leo. Donec sit amet venenatis massa. Pellentesque consequat laoreet urna sollicitudin volutpat. Integer congue felis a quam pulvinar tristique. Class aptent taciti sociosqu ad litora torquent per conubia nostra, per inceptos himenaeos. Donec fringilla pharetra justo ac tristique. Phasellus pulvinar orci a lorem eleifend, scelerisque ullamcorper purus suscipit. | You won''t know what you like best about the Antonia Racer Tank: soft, stretchy, lightweight fabric? Super-cute colorblocked details? Whatever it is, this piece is sure to quickly move to the top of your workout rotation.'),
(10, 73, 'You won''t know what you like best about the Antonia Racer Tank: soft, stretchy, lightweight fabric? Super-cute colorblocked details? Whatever it is, this piece is sure to quickly move to the top of your workout rotation. | Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed aliquam magna consequat fringilla consectetur. Duis ut elit sed nunc auctor malesuada et ac mi. Donec non diam a lectus hendrerit aliquet sed ut orci. Suspendisse et facilisis nunc. Fusce dolor eros, suscipit sit amet varius et, iaculis vitae leo. Donec sit amet venenatis massa. Pellentesque consequat laoreet urna sollicitudin volutpat. Integer congue felis a quam pulvinar tristique. Class aptent taciti sociosqu ad litora torquent per conubia nostra, per inceptos himenaeos. Donec fringilla pharetra justo ac tristique. Phasellus pulvinar orci a lorem eleifend, scelerisque ullamcorper purus suscipit. | You won''t know what you like best about the Antonia Racer Tank: soft, stretchy, lightweight fabric? Super-cute colorblocked details? Whatever it is, this piece is sure to quickly move to the top of your workout rotation.'),
(12, 70, 'Ariel Roll Sleeve Sweatshirt women'),
(12, 71, 'Ariel Roll Sleeve Sweatshirt women'),
(12, 72, 'You won''t know what you like best about the Antonia Racer Tank: soft, stretchy, lightweight fabric? Super-cute colorblocked details? Whatever it is, this piece is sure to quickly move to the top of your workout rotation. You won''t know what you like best about the Antonia Racer Tank: soft, stretchy, lightweight fabric? Super-cute colorblocked details? Whatever it is, this piece is sure to quickly move to the top of your workout rotation. You won''t know what you like best about the Antonia Racer Tank: soft, stretchy, lightweight fabric? Super-cute colorblocked details? Whatever it is, this piece is sure to quickly move to the top of your workout rotation.'),
(12, 73, 'You won''t know what you like best about the Antonia Racer Tank: soft, stretchy, lightweight fabric? Super-cute colorblocked details? Whatever it is, this piece is sure to quickly move to the top of your workout rotation.'),
(12, 90, 'blue');

-- --------------------------------------------------------

--
-- Table structure for table `catalog_category_entity`
--

CREATE TABLE `catalog_category_entity` (
  `entity_id` int(10) UNSIGNED NOT NULL COMMENT 'Entity ID',
  `attribute_set_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Attriute Set ID',
  `parent_id` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Parent Category ID',
  `created_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT 'Creation Time',
  `updated_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP COMMENT 'Update Time',
  `path` varchar(255) NOT NULL COMMENT 'Tree Path',
  `position` int(11) NOT NULL COMMENT 'Position',
  `level` int(11) NOT NULL DEFAULT '0' COMMENT 'Tree Level',
  `children_count` int(11) NOT NULL COMMENT 'Child Count'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Catalog Category Table';

--
-- Dumping data for table `catalog_category_entity`
--

INSERT INTO `catalog_category_entity` (`entity_id`, `attribute_set_id`, `parent_id`, `created_at`, `updated_at`, `path`, `position`, `level`, `children_count`) VALUES
(1, 0, 0, '2016-04-12 14:15:58', '2016-04-23 07:29:15', '1', 0, 0, 6),
(2, 3, 1, '2016-04-12 14:16:01', '2016-04-23 07:29:15', '1/2', 1, 1, 5),
(3, 3, 2, '2016-04-12 15:05:14', '2016-04-18 09:57:56', '1/2/3', 1, 2, 0),
(4, 3, 2, '2016-04-12 15:08:10', '2016-04-18 09:58:11', '1/2/4', 2, 2, 0),
(5, 3, 2, '2016-04-12 15:10:04', '2016-04-18 09:58:27', '1/2/5', 3, 2, 0),
(6, 3, 2, '2016-04-23 04:19:53', '2016-04-23 04:24:20', '1/2/6', 4, 2, 0),
(7, 3, 2, '2016-04-23 07:25:18', '2016-04-23 07:38:59', '1/2/7', 5, 2, 0);

-- --------------------------------------------------------

--
-- Table structure for table `catalog_category_entity_datetime`
--

CREATE TABLE `catalog_category_entity_datetime` (
  `value_id` int(11) NOT NULL COMMENT 'Value ID',
  `attribute_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Attribute ID',
  `store_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Store ID',
  `entity_id` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Entity ID',
  `value` datetime DEFAULT NULL COMMENT 'Value'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Catalog Category Datetime Attribute Backend Table';

--
-- Dumping data for table `catalog_category_entity_datetime`
--

INSERT INTO `catalog_category_entity_datetime` (`value_id`, `attribute_id`, `store_id`, `entity_id`, `value`) VALUES
(1, 58, 0, 1, NULL),
(2, 58, 0, 2, NULL),
(3, 58, 0, 3, NULL),
(4, 59, 0, 3, NULL),
(7, 58, 0, 4, NULL),
(8, 59, 0, 4, NULL),
(9, 58, 0, 5, NULL),
(10, 59, 0, 5, NULL),
(11, 58, 0, 6, NULL),
(12, 59, 0, 6, NULL),
(17, 58, 0, 7, NULL),
(18, 59, 0, 7, NULL);

-- --------------------------------------------------------

--
-- Table structure for table `catalog_category_entity_decimal`
--

CREATE TABLE `catalog_category_entity_decimal` (
  `value_id` int(11) NOT NULL COMMENT 'Value ID',
  `attribute_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Attribute ID',
  `store_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Store ID',
  `entity_id` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Entity ID',
  `value` decimal(12,4) DEFAULT NULL COMMENT 'Value'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Catalog Category Decimal Attribute Backend Table';

--
-- Dumping data for table `catalog_category_entity_decimal`
--

INSERT INTO `catalog_category_entity_decimal` (`value_id`, `attribute_id`, `store_id`, `entity_id`, `value`) VALUES
(1, 69, 0, 3, NULL),
(2, 69, 0, 4, NULL),
(3, 69, 0, 5, NULL),
(4, 69, 0, 6, NULL),
(5, 69, 0, 7, NULL);

-- --------------------------------------------------------

--
-- Table structure for table `catalog_category_entity_int`
--

CREATE TABLE `catalog_category_entity_int` (
  `value_id` int(11) NOT NULL COMMENT 'Value ID',
  `attribute_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Attribute ID',
  `store_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Store ID',
  `entity_id` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Entity ID',
  `value` int(11) DEFAULT NULL COMMENT 'Value'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Catalog Category Integer Attribute Backend Table';

--
-- Dumping data for table `catalog_category_entity_int`
--

INSERT INTO `catalog_category_entity_int` (`value_id`, `attribute_id`, `store_id`, `entity_id`, `value`) VALUES
(1, 66, 0, 1, 1),
(2, 43, 0, 2, 1),
(3, 66, 0, 2, 1),
(4, 43, 0, 3, 1),
(5, 66, 0, 3, 1),
(6, 50, 0, 3, NULL),
(7, 51, 0, 3, 1),
(8, 67, 0, 3, 0),
(9, 68, 0, 3, 0),
(11, 43, 0, 4, 1),
(12, 66, 0, 4, 1),
(13, 50, 0, 4, NULL),
(14, 51, 0, 4, 1),
(15, 67, 0, 4, 0),
(16, 68, 0, 4, 0),
(17, 43, 0, 5, 1),
(18, 66, 0, 5, 1),
(19, 50, 0, 5, NULL),
(20, 51, 0, 5, 1),
(21, 67, 0, 5, 0),
(22, 68, 0, 5, 0),
(23, 43, 0, 6, 1),
(24, 66, 0, 6, 1),
(25, 50, 0, 6, 10),
(26, 51, 0, 6, 1),
(27, 67, 0, 6, 0),
(28, 68, 0, 6, 0),
(30, 43, 0, 7, 1),
(31, 66, 0, 7, 1),
(32, 50, 0, 7, 11),
(33, 51, 0, 7, 1),
(34, 67, 0, 7, 0),
(35, 68, 0, 7, 0);

-- --------------------------------------------------------

--
-- Table structure for table `catalog_category_entity_text`
--

CREATE TABLE `catalog_category_entity_text` (
  `value_id` int(11) NOT NULL COMMENT 'Value ID',
  `attribute_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Attribute ID',
  `store_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Store ID',
  `entity_id` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Entity ID',
  `value` text COMMENT 'Value'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Catalog Category Text Attribute Backend Table';

--
-- Dumping data for table `catalog_category_entity_text`
--

INSERT INTO `catalog_category_entity_text` (`value_id`, `attribute_id`, `store_id`, `entity_id`, `value`) VALUES
(1, 64, 0, 1, NULL),
(2, 64, 0, 2, NULL),
(3, 44, 0, 3, NULL),
(4, 47, 0, 3, NULL),
(5, 48, 0, 3, NULL),
(6, 64, 0, 3, NULL),
(7, 61, 0, 3, NULL),
(13, 44, 0, 4, NULL),
(14, 47, 0, 4, NULL),
(15, 48, 0, 4, NULL),
(16, 64, 0, 4, NULL),
(17, 61, 0, 4, NULL),
(18, 44, 0, 5, NULL),
(19, 47, 0, 5, NULL),
(20, 48, 0, 5, NULL),
(21, 64, 0, 5, NULL),
(22, 61, 0, 5, NULL),
(23, 44, 0, 6, NULL),
(24, 47, 0, 6, NULL),
(25, 48, 0, 6, NULL),
(26, 64, 0, 6, NULL),
(27, 61, 0, 6, NULL),
(38, 44, 0, 7, NULL),
(39, 47, 0, 7, NULL),
(40, 48, 0, 7, NULL),
(41, 64, 0, 7, NULL),
(42, 61, 0, 7, NULL);

-- --------------------------------------------------------

--
-- Table structure for table `catalog_category_entity_varchar`
--

CREATE TABLE `catalog_category_entity_varchar` (
  `value_id` int(11) NOT NULL COMMENT 'Value ID',
  `attribute_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Attribute ID',
  `store_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Store ID',
  `entity_id` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Entity ID',
  `value` varchar(255) DEFAULT NULL COMMENT 'Value'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Catalog Category Varchar Attribute Backend Table';

--
-- Dumping data for table `catalog_category_entity_varchar`
--

INSERT INTO `catalog_category_entity_varchar` (`value_id`, `attribute_id`, `store_id`, `entity_id`, `value`) VALUES
(1, 42, 0, 1, 'Root Catalog'),
(2, 42, 0, 2, 'Default Category'),
(3, 49, 0, 2, 'PRODUCTS'),
(4, 42, 0, 3, 'Women'),
(5, 113, 0, 3, 'women'),
(6, 46, 0, 3, NULL),
(7, 49, 0, 3, 'PRODUCTS'),
(8, 57, 0, 3, NULL),
(9, 60, 0, 3, NULL),
(10, 65, 0, 3, NULL),
(11, 114, 0, 3, 'women'),
(20, 42, 0, 4, 'Mens'),
(21, 113, 0, 4, 'mens'),
(22, 46, 0, 4, NULL),
(23, 49, 0, 4, 'PRODUCTS'),
(24, 57, 0, 4, NULL),
(25, 60, 0, 4, NULL),
(26, 65, 0, 4, NULL),
(27, 114, 0, 4, 'mens'),
(29, 42, 0, 5, 'Accessories'),
(30, 113, 0, 5, 'accessories'),
(31, 46, 0, 5, NULL),
(32, 49, 0, 5, 'PRODUCTS'),
(33, 57, 0, 5, NULL),
(34, 60, 0, 5, NULL),
(35, 65, 0, 5, NULL),
(36, 114, 0, 5, 'accessories'),
(37, 42, 0, 6, 'Blog'),
(38, 113, 0, 6, 'blog'),
(39, 46, 0, 6, NULL),
(40, 49, 0, 6, 'PAGE'),
(41, 57, 0, 6, '4'),
(42, 60, 0, 6, '1column'),
(43, 65, 0, 6, NULL),
(44, 114, 0, 6, 'blog'),
(54, 42, 0, 7, 'About us'),
(55, 113, 0, 7, 'about-us'),
(56, 46, 0, 7, NULL),
(57, 49, 0, 7, 'PAGE'),
(58, 57, 0, 7, '4'),
(59, 60, 0, 7, '1column'),
(60, 65, 0, 7, NULL),
(61, 114, 0, 7, 'about-us');

-- --------------------------------------------------------

--
-- Table structure for table `catalog_category_product`
--

CREATE TABLE `catalog_category_product` (
  `category_id` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Category ID',
  `product_id` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Product ID',
  `position` int(11) NOT NULL DEFAULT '0' COMMENT 'Position'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Catalog Product To Category Linkage Table';

--
-- Dumping data for table `catalog_category_product`
--

INSERT INTO `catalog_category_product` (`category_id`, `product_id`, `position`) VALUES
(2, 1, 1),
(3, 1, 1),
(3, 2, 1),
(3, 3, 1),
(3, 4, 1),
(3, 5, 1),
(3, 6, 1),
(3, 7, 1),
(3, 8, 1),
(3, 9, 1),
(3, 12, 1),
(4, 1, 1),
(4, 2, 1),
(4, 3, 1),
(4, 4, 1),
(4, 5, 1),
(4, 6, 1),
(4, 7, 1),
(4, 8, 1),
(4, 9, 1),
(4, 12, 1),
(5, 1, 1),
(5, 2, 1),
(5, 3, 1),
(5, 4, 1),
(5, 5, 1),
(5, 6, 1),
(5, 7, 1),
(5, 8, 1),
(5, 9, 1),
(5, 12, 1);

-- --------------------------------------------------------

--
-- Table structure for table `catalog_category_product_index`
--

CREATE TABLE `catalog_category_product_index` (
  `category_id` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Category ID',
  `product_id` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Product ID',
  `position` int(11) DEFAULT NULL COMMENT 'Position',
  `is_parent` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Is Parent',
  `store_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Store ID',
  `visibility` smallint(5) UNSIGNED NOT NULL COMMENT 'Visibility'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Catalog Category Product Index';

--
-- Dumping data for table `catalog_category_product_index`
--

INSERT INTO `catalog_category_product_index` (`category_id`, `product_id`, `position`, `is_parent`, `store_id`, `visibility`) VALUES
(2, 10, 0, 0, 1, 4),
(2, 1, 1, 1, 1, 4),
(2, 2, 1, 1, 1, 4),
(2, 3, 1, 1, 1, 4),
(2, 4, 1, 1, 1, 4),
(2, 5, 1, 1, 1, 4),
(2, 9, 1, 1, 1, 4),
(2, 12, 1, 1, 1, 4),
(3, 1, 1, 1, 1, 4),
(3, 2, 1, 1, 1, 4),
(3, 3, 1, 1, 1, 4),
(3, 4, 1, 1, 1, 4),
(3, 5, 1, 1, 1, 4),
(3, 9, 1, 1, 1, 4),
(3, 12, 1, 1, 1, 4),
(4, 1, 1, 1, 1, 4),
(4, 2, 1, 1, 1, 4),
(4, 3, 1, 1, 1, 4),
(4, 4, 1, 1, 1, 4),
(4, 5, 1, 1, 1, 4),
(4, 9, 1, 1, 1, 4),
(4, 12, 1, 1, 1, 4),
(5, 1, 1, 1, 1, 4),
(5, 2, 1, 1, 1, 4),
(5, 3, 1, 1, 1, 4),
(5, 4, 1, 1, 1, 4),
(5, 5, 1, 1, 1, 4),
(5, 9, 1, 1, 1, 4),
(5, 12, 1, 1, 1, 4),
(2, 10, 0, 0, 2, 4),
(2, 1, 1, 1, 2, 4),
(2, 2, 1, 1, 2, 4),
(2, 3, 1, 1, 2, 4),
(2, 4, 1, 1, 2, 4),
(2, 5, 1, 1, 2, 4),
(2, 9, 1, 1, 2, 4),
(2, 12, 1, 1, 2, 4),
(3, 1, 1, 1, 2, 4),
(3, 2, 1, 1, 2, 4),
(3, 3, 1, 1, 2, 4),
(3, 4, 1, 1, 2, 4),
(3, 5, 1, 1, 2, 4),
(3, 9, 1, 1, 2, 4),
(3, 12, 1, 1, 2, 4),
(4, 1, 1, 1, 2, 4),
(4, 2, 1, 1, 2, 4),
(4, 3, 1, 1, 2, 4),
(4, 4, 1, 1, 2, 4),
(4, 5, 1, 1, 2, 4),
(4, 9, 1, 1, 2, 4),
(4, 12, 1, 1, 2, 4),
(5, 1, 1, 1, 2, 4),
(5, 2, 1, 1, 2, 4),
(5, 3, 1, 1, 2, 4),
(5, 4, 1, 1, 2, 4),
(5, 5, 1, 1, 2, 4),
(5, 9, 1, 1, 2, 4),
(5, 12, 1, 1, 2, 4);

-- --------------------------------------------------------

--
-- Table structure for table `catalog_category_product_index_tmp`
--

CREATE TABLE `catalog_category_product_index_tmp` (
  `category_id` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Category ID',
  `product_id` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Product ID',
  `position` int(11) NOT NULL DEFAULT '0' COMMENT 'Position',
  `is_parent` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Is Parent',
  `store_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Store ID',
  `visibility` smallint(5) UNSIGNED NOT NULL COMMENT 'Visibility'
) ENGINE=MEMORY DEFAULT CHARSET=utf8 COMMENT='Catalog Category Product Indexer Temp Table';

--
-- Dumping data for table `catalog_category_product_index_tmp`
--

INSERT INTO `catalog_category_product_index_tmp` (`category_id`, `product_id`, `position`, `is_parent`, `store_id`, `visibility`) VALUES
(2, 1, 1, 1, 1, 4),
(2, 2, 1, 1, 1, 4),
(2, 3, 1, 1, 1, 4),
(2, 4, 1, 1, 1, 4),
(2, 5, 1, 1, 1, 4),
(2, 9, 1, 1, 1, 4),
(2, 10, 0, 0, 1, 4),
(2, 12, 1, 1, 1, 4),
(3, 1, 1, 1, 1, 4),
(4, 1, 1, 1, 1, 4),
(5, 1, 1, 1, 1, 4),
(3, 2, 1, 1, 1, 4),
(4, 2, 1, 1, 1, 4),
(5, 2, 1, 1, 1, 4),
(3, 3, 1, 1, 1, 4),
(4, 3, 1, 1, 1, 4),
(5, 3, 1, 1, 1, 4),
(3, 4, 1, 1, 1, 4),
(4, 4, 1, 1, 1, 4),
(5, 4, 1, 1, 1, 4),
(3, 5, 1, 1, 1, 4),
(4, 5, 1, 1, 1, 4),
(5, 5, 1, 1, 1, 4),
(3, 9, 1, 1, 1, 4),
(4, 9, 1, 1, 1, 4),
(5, 9, 1, 1, 1, 4),
(3, 12, 1, 1, 1, 4),
(4, 12, 1, 1, 1, 4),
(5, 12, 1, 1, 1, 4),
(2, 1, 1, 1, 2, 4),
(2, 2, 1, 1, 2, 4),
(2, 3, 1, 1, 2, 4),
(2, 4, 1, 1, 2, 4),
(2, 5, 1, 1, 2, 4),
(2, 9, 1, 1, 2, 4),
(2, 10, 0, 0, 2, 4),
(2, 12, 1, 1, 2, 4),
(3, 1, 1, 1, 2, 4),
(4, 1, 1, 1, 2, 4),
(5, 1, 1, 1, 2, 4),
(3, 2, 1, 1, 2, 4),
(4, 2, 1, 1, 2, 4),
(5, 2, 1, 1, 2, 4),
(3, 3, 1, 1, 2, 4),
(4, 3, 1, 1, 2, 4),
(5, 3, 1, 1, 2, 4),
(3, 4, 1, 1, 2, 4),
(4, 4, 1, 1, 2, 4),
(5, 4, 1, 1, 2, 4),
(3, 5, 1, 1, 2, 4),
(4, 5, 1, 1, 2, 4),
(5, 5, 1, 1, 2, 4),
(3, 9, 1, 1, 2, 4),
(4, 9, 1, 1, 2, 4),
(5, 9, 1, 1, 2, 4),
(3, 12, 1, 1, 2, 4),
(4, 12, 1, 1, 2, 4),
(5, 12, 1, 1, 2, 4);

-- --------------------------------------------------------

--
-- Table structure for table `catalog_compare_item`
--

CREATE TABLE `catalog_compare_item` (
  `catalog_compare_item_id` int(10) UNSIGNED NOT NULL COMMENT 'Compare Item ID',
  `visitor_id` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Visitor ID',
  `customer_id` int(10) UNSIGNED DEFAULT NULL COMMENT 'Customer ID',
  `product_id` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Product ID',
  `store_id` smallint(5) UNSIGNED DEFAULT NULL COMMENT 'Store ID'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Catalog Compare Table';

--
-- Dumping data for table `catalog_compare_item`
--

INSERT INTO `catalog_compare_item` (`catalog_compare_item_id`, `visitor_id`, `customer_id`, `product_id`, `store_id`) VALUES
(1, 69, NULL, 5, 1),
(2, 69, NULL, 2, 1),
(3, 69, NULL, 1, 1),
(4, 69, NULL, 4, 1),
(5, 70, NULL, 2, 1),
(9, 161, 2, 1, 1),
(10, 161, 2, 3, 1),
(11, 161, 2, 10, 1);

-- --------------------------------------------------------

--
-- Table structure for table `catalog_eav_attribute`
--

CREATE TABLE `catalog_eav_attribute` (
  `attribute_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Attribute ID',
  `frontend_input_renderer` varchar(255) DEFAULT NULL COMMENT 'Frontend Input Renderer',
  `is_global` smallint(5) UNSIGNED NOT NULL DEFAULT '1' COMMENT 'Is Global',
  `is_visible` smallint(5) UNSIGNED NOT NULL DEFAULT '1' COMMENT 'Is Visible',
  `is_searchable` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Is Searchable',
  `is_filterable` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Is Filterable',
  `is_comparable` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Is Comparable',
  `is_visible_on_front` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Is Visible On Front',
  `is_html_allowed_on_front` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Is HTML Allowed On Front',
  `is_used_for_price_rules` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Is Used For Price Rules',
  `is_filterable_in_search` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Is Filterable In Search',
  `used_in_product_listing` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Is Used In Product Listing',
  `used_for_sort_by` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Is Used For Sorting',
  `apply_to` varchar(255) DEFAULT NULL COMMENT 'Apply To',
  `is_visible_in_advanced_search` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Is Visible In Advanced Search',
  `position` int(11) NOT NULL DEFAULT '0' COMMENT 'Position',
  `is_wysiwyg_enabled` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Is WYSIWYG Enabled',
  `is_used_for_promo_rules` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Is Used For Promo Rules',
  `is_required_in_admin_store` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Is Required In Admin Store',
  `is_used_in_grid` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Is Used in Grid',
  `is_visible_in_grid` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Is Visible in Grid',
  `is_filterable_in_grid` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Is Filterable in Grid',
  `search_weight` float NOT NULL DEFAULT '1' COMMENT 'Search Weight',
  `additional_data` text COMMENT 'Additional swatch attributes data'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Catalog EAV Attribute Table';

--
-- Dumping data for table `catalog_eav_attribute`
--

INSERT INTO `catalog_eav_attribute` (`attribute_id`, `frontend_input_renderer`, `is_global`, `is_visible`, `is_searchable`, `is_filterable`, `is_comparable`, `is_visible_on_front`, `is_html_allowed_on_front`, `is_used_for_price_rules`, `is_filterable_in_search`, `used_in_product_listing`, `used_for_sort_by`, `apply_to`, `is_visible_in_advanced_search`, `position`, `is_wysiwyg_enabled`, `is_used_for_promo_rules`, `is_required_in_admin_store`, `is_used_in_grid`, `is_visible_in_grid`, `is_filterable_in_grid`, `search_weight`, `additional_data`) VALUES
(42, NULL, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, NULL, 0, 0, 0, 0, 0, 0, 0, 0, 1, NULL),
(43, NULL, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, NULL, 0, 0, 0, 0, 0, 0, 0, 0, 1, NULL),
(44, NULL, 0, 1, 0, 0, 0, 0, 1, 0, 0, 0, 0, NULL, 0, 0, 1, 0, 0, 0, 0, 0, 1, NULL),
(45, NULL, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, NULL, 0, 0, 0, 0, 0, 0, 0, 0, 1, NULL),
(46, NULL, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, NULL, 0, 0, 0, 0, 0, 0, 0, 0, 1, NULL),
(47, NULL, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, NULL, 0, 0, 0, 0, 0, 0, 0, 0, 1, NULL),
(48, NULL, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, NULL, 0, 0, 0, 0, 0, 0, 0, 0, 1, NULL),
(49, NULL, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, NULL, 0, 0, 0, 0, 0, 0, 0, 0, 1, NULL),
(50, NULL, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, NULL, 0, 0, 0, 0, 0, 0, 0, 0, 1, NULL),
(51, NULL, 1, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, NULL, 0, 0, 0, 0, 0, 0, 0, 0, 1, NULL),
(52, NULL, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, NULL, 0, 0, 0, 0, 0, 0, 0, 0, 1, NULL),
(53, NULL, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, NULL, 0, 0, 0, 0, 0, 0, 0, 0, 1, NULL),
(54, NULL, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, NULL, 0, 0, 0, 0, 0, 0, 0, 0, 1, NULL),
(55, NULL, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, NULL, 0, 0, 0, 0, 0, 0, 0, 0, 1, NULL),
(56, NULL, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, NULL, 0, 0, 0, 0, 0, 0, 0, 0, 1, NULL),
(57, NULL, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, NULL, 0, 0, 0, 0, 0, 0, 0, 0, 1, NULL),
(58, NULL, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, NULL, 0, 0, 0, 0, 0, 0, 0, 0, 1, NULL),
(59, NULL, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, NULL, 0, 0, 0, 0, 0, 0, 0, 0, 1, NULL),
(60, NULL, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, NULL, 0, 0, 0, 0, 0, 0, 0, 0, 1, NULL),
(61, NULL, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, NULL, 0, 0, 0, 0, 0, 0, 0, 0, 1, NULL),
(62, NULL, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, NULL, 0, 0, 0, 0, 0, 0, 0, 0, 1, NULL),
(63, NULL, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, NULL, 0, 0, 0, 0, 0, 0, 0, 0, 1, NULL),
(64, 'Magento\\Catalog\\Block\\Adminhtml\\Category\\Helper\\Sortby\\Available', 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, NULL, 0, 0, 0, 0, 0, 0, 0, 0, 1, NULL),
(65, 'Magento\\Catalog\\Block\\Adminhtml\\Category\\Helper\\Sortby\\DefaultSortby', 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, NULL, 0, 0, 0, 0, 0, 0, 0, 0, 1, NULL),
(66, NULL, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, NULL, 0, 0, 0, 0, 0, 0, 0, 0, 1, NULL),
(67, NULL, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, NULL, 0, 0, 0, 0, 0, 0, 0, 0, 1, NULL),
(68, NULL, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, NULL, 0, 0, 0, 0, 0, 0, 0, 0, 1, NULL),
(69, 'Magento\\Catalog\\Block\\Adminhtml\\Category\\Helper\\Pricestep', 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, NULL, 0, 0, 0, 0, 0, 0, 0, 0, 1, NULL),
(70, NULL, 0, 1, 1, 0, 0, 0, 0, 0, 0, 1, 1, NULL, 1, 0, 0, 0, 0, 0, 0, 0, 5, NULL),
(71, NULL, 1, 1, 1, 0, 1, 0, 0, 0, 0, 0, 0, NULL, 1, 0, 0, 0, 0, 0, 0, 0, 6, NULL),
(72, NULL, 0, 1, 1, 0, 1, 0, 1, 0, 0, 0, 0, NULL, 1, 0, 1, 0, 0, 0, 0, 0, 1, NULL),
(73, NULL, 0, 1, 1, 0, 1, 0, 1, 0, 0, 1, 0, NULL, 1, 0, 1, 0, 0, 1, 0, 0, 1, NULL),
(74, NULL, 2, 1, 1, 1, 0, 0, 0, 0, 0, 1, 1, 'simple,virtual,bundle,downloadable,configurable', 1, 0, 0, 0, 0, 0, 0, 0, 1, NULL),
(75, NULL, 2, 1, 0, 0, 0, 0, 0, 0, 0, 1, 0, 'simple,virtual,bundle,downloadable,configurable', 0, 0, 0, 0, 0, 1, 0, 1, 1, NULL),
(76, NULL, 2, 1, 0, 0, 0, 0, 0, 0, 0, 1, 0, 'simple,virtual,bundle,downloadable,configurable', 0, 0, 0, 0, 0, 1, 0, 0, 1, NULL),
(77, NULL, 2, 1, 0, 0, 0, 0, 0, 0, 0, 1, 0, 'simple,virtual,bundle,downloadable,configurable', 0, 0, 0, 0, 0, 1, 0, 0, 1, NULL),
(78, NULL, 2, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 'simple,virtual,downloadable', 0, 0, 0, 0, 0, 1, 0, 1, 1, NULL),
(79, 'Magento\\Catalog\\Block\\Adminhtml\\Product\\Helper\\Form\\Weight', 1, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 'simple,virtual,bundle,downloadable,configurable', 0, 0, 0, 0, 0, 1, 0, 1, 1, NULL),
(80, NULL, 1, 1, 1, 1, 1, 0, 0, 0, 0, 0, 0, 'simple', 1, 0, 0, 0, 0, 1, 0, 1, 1, NULL),
(81, NULL, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, NULL, 0, 0, 0, 0, 0, 1, 0, 1, 1, NULL),
(82, NULL, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, NULL, 0, 0, 0, 0, 0, 1, 0, 1, 1, NULL),
(83, NULL, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, NULL, 0, 0, 0, 0, 0, 1, 0, 1, 1, NULL),
(84, 'Magento\\Catalog\\Block\\Adminhtml\\Product\\Helper\\Form\\BaseImage', 0, 1, 0, 0, 0, 0, 0, 0, 0, 1, 0, NULL, 0, 0, 0, 0, 0, 0, 0, 0, 1, NULL),
(85, NULL, 0, 1, 0, 0, 0, 0, 0, 0, 0, 1, 0, NULL, 0, 0, 0, 0, 0, 0, 0, 0, 1, NULL),
(86, NULL, 0, 1, 0, 0, 0, 0, 0, 0, 0, 1, 0, NULL, 0, 0, 0, 0, 0, 0, 0, 0, 1, NULL),
(87, NULL, 1, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, NULL, 0, 0, 0, 0, 0, 0, 0, 0, 1, NULL),
(88, NULL, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, NULL, 0, 0, 0, 0, 0, 0, 0, 0, 1, NULL),
(89, NULL, 2, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 'simple,virtual,bundle,downloadable,configurable', 0, 0, 0, 0, 0, 0, 0, 0, 1, NULL),
(90, NULL, 1, 1, 1, 1, 1, 0, 0, 0, 0, 0, 0, 'simple,virtual,configurable', 1, 0, 0, 0, 0, 1, 0, 1, 1, NULL),
(91, NULL, 2, 1, 0, 0, 0, 0, 0, 0, 0, 1, 0, NULL, 0, 0, 0, 0, 0, 1, 0, 0, 1, NULL),
(92, NULL, 2, 1, 0, 0, 0, 0, 0, 0, 0, 1, 0, NULL, 0, 0, 0, 0, 0, 1, 0, 0, 1, NULL),
(93, NULL, 1, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, NULL, 0, 0, 0, 0, 0, 0, 0, 0, 1, NULL),
(94, 'Magento\\Framework\\Data\\Form\\Element\\Hidden', 2, 1, 1, 0, 0, 0, 0, 0, 0, 1, 0, NULL, 0, 0, 0, 0, 1, 0, 0, 0, 1, NULL),
(95, NULL, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 'simple,virtual,bundle,downloadable,configurable', 0, 0, 0, 0, 0, 0, 0, 0, 1, NULL),
(96, NULL, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, NULL, 0, 0, 0, 0, 1, 0, 0, 0, 1, NULL),
(97, NULL, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, NULL, 0, 0, 0, 0, 0, 1, 0, 1, 1, NULL),
(98, NULL, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, NULL, 0, 0, 0, 0, 0, 1, 0, 0, 1, NULL),
(99, NULL, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, NULL, 0, 0, 0, 0, 0, 1, 0, 0, 1, NULL),
(100, NULL, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, NULL, 0, 0, 0, 0, 0, 0, 0, 0, 1, NULL),
(101, NULL, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, NULL, 0, 0, 0, 0, 0, 1, 0, 0, 1, NULL),
(102, 'Magento\\Catalog\\Block\\Adminhtml\\Product\\Helper\\Form\\Category', 1, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, NULL, 0, 0, 0, 0, 0, 0, 0, 0, 1, NULL),
(103, NULL, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, NULL, 0, 0, 0, 0, 0, 0, 0, 0, 1, NULL),
(104, NULL, 1, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, NULL, 0, 0, 0, 0, 0, 0, 0, 0, 1, NULL),
(105, NULL, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, NULL, 0, 0, 0, 0, 0, 0, 0, 0, 1, NULL),
(106, NULL, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, NULL, 0, 0, 0, 0, 0, 0, 0, 0, 1, NULL),
(107, NULL, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, NULL, 0, 0, 0, 0, 0, 0, 0, 0, 1, NULL),
(108, NULL, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, NULL, 0, 0, 0, 0, 0, 0, 0, 0, 1, NULL),
(109, NULL, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, NULL, 0, 0, 0, 0, 0, 0, 0, 0, 1, NULL),
(110, NULL, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, NULL, 0, 0, 0, 0, 0, 0, 0, 0, 1, NULL),
(111, NULL, 2, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 'simple,bundle,grouped,configurable', 0, 0, 0, 0, 0, 1, 0, 1, 1, NULL),
(112, 'Magento\\CatalogInventory\\Block\\Adminhtml\\Form\\Field\\Stock', 1, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, NULL, 0, 0, 0, 0, 0, 0, 0, 0, 1, NULL),
(113, NULL, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, NULL, 0, 0, 0, 0, 0, 0, 0, 0, 1, NULL),
(114, NULL, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, NULL, 0, 0, 0, 0, 0, 0, 0, 0, 1, NULL),
(115, NULL, 0, 1, 0, 0, 0, 0, 0, 0, 0, 1, 0, NULL, 0, 0, 0, 0, 0, 1, 0, 1, 1, NULL),
(116, NULL, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, NULL, 0, 0, 0, 0, 0, 0, 0, 0, 1, NULL),
(117, 'Magento\\Msrp\\Block\\Adminhtml\\Product\\Helper\\Form\\Type', 2, 1, 0, 0, 0, 0, 0, 0, 0, 1, 0, 'simple,virtual,downloadable,bundle,configurable', 0, 0, 0, 0, 0, 1, 0, 1, 1, NULL),
(118, 'Magento\\Msrp\\Block\\Adminhtml\\Product\\Helper\\Form\\Type\\Price', 2, 1, 0, 0, 0, 0, 0, 0, 0, 1, 0, 'simple,virtual,downloadable,bundle,configurable', 0, 0, 0, 0, 0, 0, 0, 0, 1, NULL),
(119, NULL, 1, 1, 0, 0, 0, 0, 0, 0, 0, 1, 0, 'bundle', 0, 0, 0, 0, 0, 0, 0, 0, 1, NULL),
(120, NULL, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 'bundle', 0, 0, 0, 0, 0, 0, 0, 0, 1, NULL),
(121, NULL, 1, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 'bundle', 0, 0, 0, 0, 0, 0, 0, 0, 1, NULL),
(122, NULL, 1, 1, 0, 0, 0, 0, 0, 0, 0, 1, 0, 'bundle', 0, 0, 0, 0, 0, 0, 0, 0, 1, NULL),
(123, NULL, 1, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 'bundle', 0, 0, 0, 0, 0, 0, 0, 0, 1, NULL),
(124, NULL, 1, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 'downloadable', 0, 0, 0, 0, 0, 0, 0, 0, 1, NULL),
(125, NULL, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 'downloadable', 0, 0, 0, 0, 0, 0, 0, 0, 1, NULL),
(126, NULL, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 'downloadable', 0, 0, 0, 0, 0, 0, 0, 0, 1, NULL),
(127, NULL, 1, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 'downloadable', 0, 0, 0, 0, 0, 0, 0, 0, 1, NULL),
(128, NULL, 0, 1, 0, 0, 0, 0, 0, 0, 0, 1, 0, NULL, 0, 0, 0, 0, 0, 0, 0, 0, 1, NULL),
(129, NULL, 2, 1, 1, 0, 0, 0, 0, 0, 0, 1, 0, 'simple,virtual,bundle,downloadable,configurable', 0, 0, 0, 0, 0, 1, 0, 1, 1, NULL),
(130, 'Magento\\GiftMessage\\Block\\Adminhtml\\Product\\Helper\\Form\\Config', 1, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, NULL, 0, 0, 0, 0, 0, 1, 0, 0, 1, NULL);

-- --------------------------------------------------------

--
-- Table structure for table `catalog_product_bundle_option`
--

CREATE TABLE `catalog_product_bundle_option` (
  `option_id` int(10) UNSIGNED NOT NULL COMMENT 'Option Id',
  `parent_id` int(10) UNSIGNED NOT NULL COMMENT 'Parent Id',
  `required` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Required',
  `position` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Position',
  `type` varchar(255) DEFAULT NULL COMMENT 'Type'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Catalog Product Bundle Option';

--
-- Dumping data for table `catalog_product_bundle_option`
--

INSERT INTO `catalog_product_bundle_option` (`option_id`, `parent_id`, `required`, `position`, `type`) VALUES
(1, 9, 1, 0, 'checkbox');

-- --------------------------------------------------------

--
-- Table structure for table `catalog_product_bundle_option_value`
--

CREATE TABLE `catalog_product_bundle_option_value` (
  `value_id` int(10) UNSIGNED NOT NULL COMMENT 'Value Id',
  `option_id` int(10) UNSIGNED NOT NULL COMMENT 'Option Id',
  `store_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Store Id',
  `title` varchar(255) DEFAULT NULL COMMENT 'Title'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Catalog Product Bundle Option Value';

--
-- Dumping data for table `catalog_product_bundle_option_value`
--

INSERT INTO `catalog_product_bundle_option_value` (`value_id`, `option_id`, `store_id`, `title`) VALUES
(3, 1, 0, 'Custom option name');

-- --------------------------------------------------------

--
-- Table structure for table `catalog_product_bundle_price_index`
--

CREATE TABLE `catalog_product_bundle_price_index` (
  `entity_id` int(10) UNSIGNED NOT NULL COMMENT 'Entity Id',
  `website_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Website Id',
  `customer_group_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Customer Group Id',
  `min_price` decimal(12,4) NOT NULL COMMENT 'Min Price',
  `max_price` decimal(12,4) NOT NULL COMMENT 'Max Price'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Catalog Product Bundle Price Index';

-- --------------------------------------------------------

--
-- Table structure for table `catalog_product_bundle_selection`
--

CREATE TABLE `catalog_product_bundle_selection` (
  `selection_id` int(10) UNSIGNED NOT NULL COMMENT 'Selection Id',
  `option_id` int(10) UNSIGNED NOT NULL COMMENT 'Option Id',
  `parent_product_id` int(10) UNSIGNED NOT NULL COMMENT 'Parent Product Id',
  `product_id` int(10) UNSIGNED NOT NULL COMMENT 'Product Id',
  `position` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Position',
  `is_default` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Is Default',
  `selection_price_type` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Selection Price Type',
  `selection_price_value` decimal(12,4) NOT NULL DEFAULT '0.0000' COMMENT 'Selection Price Value',
  `selection_qty` decimal(12,4) DEFAULT NULL COMMENT 'Selection Qty',
  `selection_can_change_qty` smallint(6) NOT NULL DEFAULT '0' COMMENT 'Selection Can Change Qty'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Catalog Product Bundle Selection';

--
-- Dumping data for table `catalog_product_bundle_selection`
--

INSERT INTO `catalog_product_bundle_selection` (`selection_id`, `option_id`, `parent_product_id`, `product_id`, `position`, `is_default`, `selection_price_type`, `selection_price_value`, `selection_qty`, `selection_can_change_qty`) VALUES
(1, 1, 9, 1, 0, 0, 0, '0.0000', '1.0000', 1),
(2, 1, 9, 6, 1, 0, 0, '0.0000', '1.0000', 1);

-- --------------------------------------------------------

--
-- Table structure for table `catalog_product_bundle_selection_price`
--

CREATE TABLE `catalog_product_bundle_selection_price` (
  `selection_id` int(10) UNSIGNED NOT NULL COMMENT 'Selection Id',
  `website_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Website Id',
  `selection_price_type` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Selection Price Type',
  `selection_price_value` decimal(12,4) NOT NULL DEFAULT '0.0000' COMMENT 'Selection Price Value'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Catalog Product Bundle Selection Price';

-- --------------------------------------------------------

--
-- Table structure for table `catalog_product_bundle_stock_index`
--

CREATE TABLE `catalog_product_bundle_stock_index` (
  `entity_id` int(10) UNSIGNED NOT NULL COMMENT 'Entity Id',
  `website_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Website Id',
  `stock_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Stock Id',
  `option_id` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Option Id',
  `stock_status` smallint(6) DEFAULT '0' COMMENT 'Stock Status'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Catalog Product Bundle Stock Index';

-- --------------------------------------------------------

--
-- Table structure for table `catalog_product_entity`
--

CREATE TABLE `catalog_product_entity` (
  `entity_id` int(10) UNSIGNED NOT NULL COMMENT 'Entity ID',
  `attribute_set_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Attribute Set ID',
  `type_id` varchar(32) NOT NULL DEFAULT 'simple' COMMENT 'Type ID',
  `sku` varchar(64) DEFAULT NULL COMMENT 'SKU',
  `has_options` smallint(6) NOT NULL DEFAULT '0' COMMENT 'Has Options',
  `required_options` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Required Options',
  `created_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT 'Creation Time',
  `updated_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP COMMENT 'Update Time'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Catalog Product Table';

--
-- Dumping data for table `catalog_product_entity`
--

INSERT INTO `catalog_product_entity` (`entity_id`, `attribute_set_id`, `type_id`, `sku`, `has_options`, `required_options`, `created_at`, `updated_at`) VALUES
(1, 4, 'simple', 'Ariel Roll Sleeve Sweatshirt', 0, 0, '2016-04-15 10:06:44', '2016-04-29 08:20:07'),
(2, 4, 'virtual', 'Arcadio Gym Short-32-Blue', 0, 0, '2016-04-19 03:50:31', '2016-04-21 02:24:32'),
(3, 4, 'virtual', 'Atomic Endurance Running Tee', 0, 0, '2016-04-19 04:25:36', '2016-04-21 02:26:00'),
(4, 4, 'virtual', 'Arcadio Gym Short', 0, 0, '2016-04-19 06:48:01', '2016-04-21 02:13:16'),
(5, 4, 'configurable', 'product configuration magento', 1, 1, '2016-04-19 07:21:37', '2016-04-21 02:17:57'),
(6, 4, 'virtual', 'product configuration magento-blue', 0, 0, '2016-04-19 07:24:22', '2016-04-19 07:24:22'),
(7, 4, 'virtual', 'product configuration magento-pink', 0, 0, '2016-04-19 07:24:24', '2016-04-19 07:24:24'),
(8, 4, 'virtual', 'product configuration magento-red', 0, 0, '2016-04-19 07:24:25', '2016-04-19 07:24:25'),
(9, 4, 'bundle', 'Magento Bundle Product Type', 1, 1, '2016-04-25 02:13:21', '2016-04-25 02:25:39'),
(10, 4, 'grouped', 'Grouped products ', 0, 0, '2016-04-25 02:33:18', '2016-04-25 02:35:48'),
(12, 4, 'simple', ' Ariel Roll Sleeve Sweatshirt women', 0, 0, '2016-04-25 02:50:41', '2016-04-25 03:00:54');

-- --------------------------------------------------------

--
-- Table structure for table `catalog_product_entity_datetime`
--

CREATE TABLE `catalog_product_entity_datetime` (
  `value_id` int(11) NOT NULL COMMENT 'Value ID',
  `attribute_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Attribute ID',
  `store_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Store ID',
  `entity_id` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Entity ID',
  `value` datetime DEFAULT NULL COMMENT 'Value'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Catalog Product Datetime Attribute Backend Table';

--
-- Dumping data for table `catalog_product_entity_datetime`
--

INSERT INTO `catalog_product_entity_datetime` (`value_id`, `attribute_id`, `store_id`, `entity_id`, `value`) VALUES
(1, 76, 0, 1, NULL),
(2, 77, 0, 1, NULL),
(3, 98, 0, 1, NULL),
(4, 99, 0, 1, NULL),
(5, 91, 0, 1, NULL),
(6, 92, 0, 1, NULL),
(7, 76, 0, 2, NULL),
(8, 77, 0, 2, NULL),
(9, 98, 0, 2, NULL),
(10, 99, 0, 2, NULL),
(11, 91, 0, 2, NULL),
(12, 92, 0, 2, NULL),
(37, 76, 0, 3, NULL),
(38, 77, 0, 3, NULL),
(39, 98, 0, 3, NULL),
(40, 99, 0, 3, NULL),
(41, 91, 0, 3, NULL),
(42, 92, 0, 3, NULL),
(43, 76, 0, 4, NULL),
(44, 77, 0, 4, NULL),
(45, 98, 0, 4, NULL),
(46, 99, 0, 4, NULL),
(47, 91, 0, 4, NULL),
(48, 92, 0, 4, NULL),
(49, 98, 0, 5, NULL),
(50, 99, 0, 5, NULL),
(51, 91, 0, 5, NULL),
(52, 92, 0, 5, NULL),
(53, 76, 0, 5, NULL),
(54, 76, 0, 6, NULL),
(55, 77, 0, 6, NULL),
(56, 98, 0, 6, NULL),
(57, 99, 0, 6, NULL),
(58, 91, 0, 6, NULL),
(59, 92, 0, 6, NULL),
(60, 76, 0, 7, NULL),
(61, 77, 0, 7, NULL),
(62, 98, 0, 7, NULL),
(63, 99, 0, 7, NULL),
(64, 91, 0, 7, NULL),
(65, 92, 0, 7, NULL),
(66, 76, 0, 8, NULL),
(67, 77, 0, 8, NULL),
(68, 98, 0, 8, NULL),
(69, 99, 0, 8, NULL),
(70, 91, 0, 8, NULL),
(71, 92, 0, 8, NULL),
(72, 77, 0, 5, NULL),
(73, 76, 0, 9, NULL),
(74, 77, 0, 9, NULL),
(75, 98, 0, 9, NULL),
(76, 99, 0, 9, NULL),
(77, 91, 0, 9, NULL),
(78, 92, 0, 9, NULL),
(97, 98, 0, 10, NULL),
(98, 99, 0, 10, NULL),
(99, 91, 0, 10, NULL),
(100, 92, 0, 10, NULL),
(111, 76, 0, 12, NULL),
(112, 77, 0, 12, NULL),
(113, 98, 0, 12, NULL),
(114, 99, 0, 12, NULL),
(115, 91, 0, 12, NULL),
(116, 92, 0, 12, NULL);

-- --------------------------------------------------------

--
-- Table structure for table `catalog_product_entity_decimal`
--

CREATE TABLE `catalog_product_entity_decimal` (
  `value_id` int(11) NOT NULL COMMENT 'Value ID',
  `attribute_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Attribute ID',
  `store_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Store ID',
  `entity_id` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Entity ID',
  `value` decimal(12,4) DEFAULT NULL COMMENT 'Value'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Catalog Product Decimal Attribute Backend Table';

--
-- Dumping data for table `catalog_product_entity_decimal`
--

INSERT INTO `catalog_product_entity_decimal` (`value_id`, `attribute_id`, `store_id`, `entity_id`, `value`) VALUES
(1, 74, 0, 1, '150.0000'),
(2, 79, 0, 1, NULL),
(3, 75, 0, 1, NULL),
(4, 78, 0, 1, NULL),
(5, 74, 0, 2, '25.0000'),
(6, 79, 0, 2, NULL),
(7, 75, 0, 2, NULL),
(8, 78, 0, 2, NULL),
(21, 74, 0, 3, '25.0000'),
(22, 75, 0, 3, NULL),
(23, 78, 0, 3, NULL),
(24, 74, 0, 4, '24.0000'),
(25, 75, 0, 4, NULL),
(26, 78, 0, 4, NULL),
(27, 79, 0, 4, NULL),
(28, 74, 0, 5, '120.0000'),
(29, 79, 0, 5, NULL),
(30, 74, 0, 6, '120.0000'),
(31, 79, 0, 6, NULL),
(32, 75, 0, 6, NULL),
(33, 78, 0, 6, NULL),
(34, 117, 0, 6, NULL),
(35, 74, 0, 7, '120.0000'),
(36, 79, 0, 7, NULL),
(37, 75, 0, 7, NULL),
(38, 78, 0, 7, NULL),
(39, 117, 0, 7, NULL),
(40, 74, 0, 8, '120.0000'),
(41, 79, 0, 8, NULL),
(42, 75, 0, 8, NULL),
(43, 78, 0, 8, NULL),
(44, 117, 0, 8, NULL),
(45, 75, 0, 5, NULL),
(54, 79, 0, 3, NULL),
(55, 75, 0, 9, NULL),
(56, 74, 0, 9, '50.0000'),
(63, 74, 0, 12, '80.0000'),
(64, 79, 0, 12, NULL),
(65, 75, 0, 12, NULL),
(66, 78, 0, 12, NULL);

-- --------------------------------------------------------

--
-- Table structure for table `catalog_product_entity_gallery`
--

CREATE TABLE `catalog_product_entity_gallery` (
  `value_id` int(11) NOT NULL COMMENT 'Value ID',
  `attribute_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Attribute ID',
  `store_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Store ID',
  `entity_id` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Entity ID',
  `position` int(11) NOT NULL DEFAULT '0' COMMENT 'Position',
  `value` varchar(255) DEFAULT NULL COMMENT 'Value'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Catalog Product Gallery Attribute Backend Table';

-- --------------------------------------------------------

--
-- Table structure for table `catalog_product_entity_int`
--

CREATE TABLE `catalog_product_entity_int` (
  `value_id` int(11) NOT NULL COMMENT 'Value ID',
  `attribute_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Attribute ID',
  `store_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Store ID',
  `entity_id` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Entity ID',
  `value` int(11) DEFAULT NULL COMMENT 'Value'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Catalog Product Integer Attribute Backend Table';

--
-- Dumping data for table `catalog_product_entity_int`
--

INSERT INTO `catalog_product_entity_int` (`value_id`, `attribute_id`, `store_id`, `entity_id`, `value`) VALUES
(1, 129, 0, 1, 0),
(2, 94, 0, 1, 1),
(3, 96, 0, 1, 4),
(4, 112, 0, 1, 1),
(5, 129, 0, 2, 0),
(6, 94, 0, 2, 1),
(7, 96, 0, 2, 4),
(8, 112, 0, 2, 1),
(13, 129, 0, 3, 2),
(14, 94, 0, 3, 1),
(15, 96, 0, 3, 4),
(16, 112, 0, 3, 1),
(17, 129, 0, 4, 0),
(18, 94, 0, 4, 1),
(19, 96, 0, 4, 4),
(20, 112, 0, 4, 1),
(21, 129, 0, 5, 0),
(22, 94, 0, 5, 1),
(23, 96, 0, 5, 4),
(24, 112, 0, 5, 1),
(25, 129, 0, 6, 0),
(26, 94, 0, 6, 1),
(27, 90, 0, 6, 4),
(28, 96, 0, 6, 1),
(29, 112, 0, 6, 1),
(30, 129, 0, 7, 0),
(31, 94, 0, 7, 1),
(32, 90, 0, 7, 5),
(33, 96, 0, 7, 1),
(34, 112, 0, 7, 1),
(35, 129, 0, 8, 0),
(36, 94, 0, 8, 1),
(37, 90, 0, 8, 6),
(38, 96, 0, 8, 1),
(39, 112, 0, 8, 1),
(40, 90, 0, 5, NULL),
(41, 90, 0, 4, NULL),
(43, 90, 0, 2, NULL),
(45, 90, 0, 3, NULL),
(46, 120, 0, 9, 0),
(47, 119, 0, 9, 0),
(48, 121, 0, 9, 0),
(49, 94, 0, 9, 1),
(50, 123, 0, 9, 0),
(51, 122, 0, 9, 0),
(52, 96, 0, 9, 4),
(53, 129, 0, 9, 2),
(54, 112, 0, 9, 1),
(58, 94, 0, 10, 1),
(59, 96, 0, 10, 4),
(60, 112, 0, 10, 1),
(67, 129, 0, 12, 0),
(68, 94, 0, 12, 1),
(69, 90, 0, 12, 4),
(70, 96, 0, 12, 4),
(71, 112, 0, 12, 1),
(72, 90, 0, 1, NULL);

-- --------------------------------------------------------

--
-- Table structure for table `catalog_product_entity_media_gallery`
--

CREATE TABLE `catalog_product_entity_media_gallery` (
  `value_id` int(10) UNSIGNED NOT NULL COMMENT 'Value ID',
  `attribute_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Attribute ID',
  `value` varchar(255) DEFAULT NULL COMMENT 'Value',
  `media_type` varchar(32) NOT NULL DEFAULT 'image' COMMENT 'Media entry type',
  `disabled` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Visibility status'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Catalog Product Media Gallery Attribute Backend Table';

--
-- Dumping data for table `catalog_product_entity_media_gallery`
--

INSERT INTO `catalog_product_entity_media_gallery` (`value_id`, `attribute_id`, `value`, `media_type`, `disabled`) VALUES
(1, 87, '/f/a/fasony100.jpg', 'image', 0),
(2, 87, '/f/a/fasony100_2.jpg', 'image', 0),
(3, 87, '/f/a/fasony100_1.jpg', 'image', 0),
(4, 87, '/f/a/fasony101_3.jpg', 'image', 0),
(5, 87, '/f/a/fasony101_2_1.jpg', 'image', 0),
(6, 87, '/f/a/fasony101_1_1.jpg', 'image', 0),
(7, 87, '/f/a/fasony107.jpg', 'image', 0),
(8, 87, '/f/a/fasony107_2.jpg', 'image', 0),
(9, 87, '/f/a/fasony107_1.jpg', 'image', 0),
(10, 87, '/f/a/fasony106.jpg', 'image', 0),
(11, 87, '/f/a/fasony101_1_1_1.jpg', 'image', 0),
(12, 87, '/f/a/fasony101_2_1_1.jpg', 'image', 0),
(13, 87, '/f/a/fasony105.jpg', 'image', 0),
(14, 87, '/f/a/fasony100_3.jpg', 'image', 0),
(15, 87, '/f/a/fasony106_1.jpg', 'image', 0),
(16, 87, '/f/a/fasony101_3_1.jpg', 'image', 0),
(17, 87, '/f/a/fasony104.jpg', 'image', 0),
(18, 87, '/f/a/fasony107_2_1.jpg', 'image', 0),
(19, 87, '/f/a/fasony107_3.jpg', 'image', 0),
(20, 87, '/f/a/fasony103.jpg', 'image', 0),
(21, 87, '/f/a/fasony107_1_1.jpg', 'image', 0),
(22, 87, '/f/a/fasony107_2_2.jpg', 'image', 0),
(28, 87, '/f/a/fasony102_1.jpg', 'image', 0),
(29, 87, '/f/a/fasony103_2.jpg', 'image', 0),
(30, 87, '/f/a/fasony104_1.jpg', 'image', 0),
(31, 87, '/f/a/fasony107_2_4.jpg', 'image', 0),
(32, 87, '/f/a/fasony107_4.jpg', 'image', 0);

-- --------------------------------------------------------

--
-- Table structure for table `catalog_product_entity_media_gallery_value`
--

CREATE TABLE `catalog_product_entity_media_gallery_value` (
  `value_id` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Value ID',
  `store_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Store ID',
  `entity_id` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Entity ID',
  `label` varchar(255) DEFAULT NULL COMMENT 'Label',
  `position` int(10) UNSIGNED DEFAULT NULL COMMENT 'Position',
  `disabled` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Is Disabled',
  `record_id` int(10) UNSIGNED NOT NULL COMMENT 'Record Id'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Catalog Product Media Gallery Attribute Value Table';

--
-- Dumping data for table `catalog_product_entity_media_gallery_value`
--

INSERT INTO `catalog_product_entity_media_gallery_value` (`value_id`, `store_id`, `entity_id`, `label`, `position`, `disabled`, `record_id`) VALUES
(14, 0, 6, NULL, 1, 0, 47),
(15, 0, 7, NULL, 1, 0, 48),
(16, 0, 8, NULL, 1, 0, 49),
(10, 0, 4, NULL, 1, 0, 52),
(11, 0, 4, NULL, 2, 0, 53),
(12, 0, 4, NULL, 3, 0, 54),
(13, 0, 5, NULL, 1, 0, 61),
(4, 0, 2, NULL, 1, 0, 71),
(5, 0, 2, NULL, 2, 0, 72),
(6, 0, 2, NULL, 3, 0, 73),
(7, 0, 3, NULL, 1, 0, 74),
(8, 0, 3, NULL, 2, 0, 75),
(9, 0, 3, NULL, 3, 0, 76),
(17, 0, 9, NULL, 0, 0, 86),
(18, 0, 9, NULL, 1, 0, 87),
(19, 0, 9, NULL, 2, 0, 88),
(20, 0, 10, NULL, 0, 0, 92),
(21, 0, 10, NULL, 1, 0, 93),
(22, 0, 10, NULL, 2, 0, 94),
(28, 0, 12, NULL, 6, 0, 101),
(29, 0, 12, NULL, 2, 0, 102),
(30, 0, 12, NULL, 3, 0, 103),
(31, 0, 12, NULL, 4, 0, 104),
(32, 0, 12, NULL, 5, 0, 105),
(1, 0, 1, NULL, 1, 0, 106),
(2, 0, 1, NULL, 2, 0, 107),
(3, 0, 1, NULL, 3, 0, 108);

-- --------------------------------------------------------

--
-- Table structure for table `catalog_product_entity_media_gallery_value_to_entity`
--

CREATE TABLE `catalog_product_entity_media_gallery_value_to_entity` (
  `value_id` int(10) UNSIGNED NOT NULL COMMENT 'Value media Entry ID',
  `entity_id` int(10) UNSIGNED NOT NULL COMMENT 'Product entity ID'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Link Media value to Product entity table';

--
-- Dumping data for table `catalog_product_entity_media_gallery_value_to_entity`
--

INSERT INTO `catalog_product_entity_media_gallery_value_to_entity` (`value_id`, `entity_id`) VALUES
(1, 1),
(2, 1),
(3, 1),
(4, 2),
(5, 2),
(6, 2),
(7, 3),
(8, 3),
(9, 3),
(10, 4),
(11, 4),
(12, 4),
(13, 5),
(14, 6),
(15, 7),
(16, 8),
(17, 9),
(18, 9),
(19, 9),
(20, 10),
(21, 10),
(22, 10),
(28, 12),
(29, 12),
(30, 12),
(31, 12),
(32, 12);

-- --------------------------------------------------------

--
-- Table structure for table `catalog_product_entity_media_gallery_value_video`
--

CREATE TABLE `catalog_product_entity_media_gallery_value_video` (
  `value_id` int(10) UNSIGNED NOT NULL COMMENT 'Media Entity ID',
  `store_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Store ID',
  `provider` varchar(32) DEFAULT NULL COMMENT 'Video provider ID',
  `url` text COMMENT 'Video URL',
  `title` varchar(255) DEFAULT NULL COMMENT 'Title',
  `description` text COMMENT 'Page Meta Description',
  `metadata` text COMMENT 'Video meta data'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Catalog Product Video Table';

-- --------------------------------------------------------

--
-- Table structure for table `catalog_product_entity_text`
--

CREATE TABLE `catalog_product_entity_text` (
  `value_id` int(11) NOT NULL COMMENT 'Value ID',
  `attribute_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Attribute ID',
  `store_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Store ID',
  `entity_id` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Entity ID',
  `value` text COMMENT 'Value'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Catalog Product Text Attribute Backend Table';

--
-- Dumping data for table `catalog_product_entity_text`
--

INSERT INTO `catalog_product_entity_text` (`value_id`, `attribute_id`, `store_id`, `entity_id`, `value`) VALUES
(1, 72, 0, 1, '<div class="value">\r\n<p>Soft, sleek and subtle, the Ariel Roll Sleeve Sweatshirt is a nuanced fitness garment for all occasions. It works equally well as a workout piece or in a casual social setting.</p>\r\n<p>&bull; Purple two-tone lightweight hoodie. <br />&bull; 100% cotton.<br />&bull; Adjustable roll sleeves for Long-Sleeve or 3/4 sleeve.<br />&bull; Casual, comfy piece for running errands or weekend activities.</p>\r\n</div>'),
(2, 82, 0, 1, 'Ariel Roll Sleeve Sweatshirt'),
(3, 100, 0, 1, NULL),
(4, 73, 0, 1, '<p>You won''t know what you like best about the Antonia Racer Tank: soft, stretchy, lightweight fabric? Super-cute colorblocked details? Whatever it is, this piece is sure to quickly move to the top of your workout rotation.</p>'),
(5, 72, 0, 2, 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed aliquam magna consequat fringilla consectetur. Duis ut elit sed nunc auctor malesuada et ac mi. Donec non diam a lectus hendrerit aliquet sed ut orci. Suspendisse et facilisis nunc. Fusce dolor eros, suscipit sit amet varius et, iaculis vitae leo. Donec sit amet venenatis massa. Pellentesque consequat laoreet urna sollicitudin volutpat. Integer congue felis a quam pulvinar tristique. Class aptent taciti sociosqu ad litora torquent per conubia nostra, per inceptos himenaeos. Donec fringilla pharetra justo ac tristique. Phasellus pulvinar orci a lorem eleifend, scelerisque ullamcorper purus suscipit. '),
(6, 82, 0, 2, 'Arcadio Gym Short-32-Blue'),
(7, 100, 0, 2, NULL),
(8, 73, 0, 2, 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed aliquam magna consequat fringilla consectetur. Duis ut elit sed nunc auctor malesuada et ac mi. Donec non diam a lectus hendrerit aliquet sed ut orci. Suspendisse et facilisis nunc. Fusce dolor eros, suscipit sit amet varius et, iaculis vitae leo. Donec sit amet venenatis massa. Pellentesque consequat laoreet urna sollicitudin volutpat. Integer congue felis a quam pulvinar tristique. Class aptent taciti sociosqu ad litora torquent per conubia nostra, per inceptos himenaeos. Donec fringilla pharetra justo ac tristique. Phasellus pulvinar orci a lorem eleifend, scelerisque ullamcorper purus suscipit. '),
(21, 72, 0, 3, '<p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed aliquam magna consequat fringilla consectetur. Duis ut elit sed nunc auctor malesuada et ac mi. Donec non diam a lectus hendrerit aliquet sed ut orci. Suspendisse et facilisis nunc. Fusce dolor eros, suscipit sit amet varius et, iaculis vitae leo. Donec sit amet venenatis massa. Pellentesque consequat laoreet urna sollicitudin volutpat. Integer congue felis a quam pulvinar tristique. Class aptent taciti sociosqu ad litora torquent per conubia nostra, per inceptos himenaeos. Donec fringilla pharetra justo ac tristique. Phasellus pulvinar orci a lorem eleifend, scelerisque ullamcorper purus suscipit.</p>'),
(22, 82, 0, 3, 'Atomic Endurance Running Tee'),
(23, 100, 0, 3, NULL),
(24, 73, 0, 3, '<p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed aliquam magna consequat fringilla consectetur. Duis ut elit sed nunc auctor malesuada et ac mi. Donec non diam a lectus hendrerit aliquet sed ut orci. Suspendisse et facilisis nunc. Fusce dolor eros, suscipit sit amet varius et, iaculis vitae leo. Donec sit amet venenatis massa. Pellentesque consequat laoreet urna sollicitudin volutpat. Integer congue felis a quam pulvinar tristique. Class aptent taciti sociosqu ad litora torquent per conubia nostra, per inceptos himenaeos. Donec fringilla pharetra justo ac tristique. Phasellus pulvinar orci a lorem eleifend, scelerisque ullamcorper purus suscipit.</p>'),
(25, 72, 0, 4, '<p>You won''t know what you like best about the Antonia Racer Tank: soft, stretchy, lightweight fabric? Super-cute colorblocked details? Whatever it is, this piece is sure to quickly move to the top of your workout rotation.</p>'),
(26, 82, 0, 4, 'Arcadio Gym Short'),
(27, 100, 0, 4, NULL),
(28, 73, 0, 4, '<p>You won''t know what you like best about the Antonia Racer Tank: soft, stretchy, lightweight fabric? Super-cute colorblocked details? Whatever it is, this piece is sure to quickly move to the top of your workout rotation.</p>'),
(29, 72, 0, 5, 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed aliquam magna consequat fringilla consectetur. Duis ut elit sed nunc auctor malesuada et ac mi. Donec non diam a lectus hendrerit aliquet sed ut orci. Suspendisse et facilisis nunc. Fusce dolor eros, suscipit sit amet varius et, iaculis vitae leo. Donec sit amet venenatis massa. Pellentesque consequat laoreet urna sollicitudin volutpat. Integer congue felis a quam pulvinar tristique. Class aptent taciti sociosqu ad litora torquent per conubia nostra, per inceptos himenaeos. Donec fringilla pharetra justo ac tristique. Phasellus pulvinar orci a lorem eleifend, scelerisque ullamcorper purus suscipit. '),
(30, 82, 0, 5, 'product configuration magento'),
(31, 100, 0, 5, NULL),
(32, 73, 0, 5, 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed aliquam magna consequat fringilla consectetur. Duis ut elit sed nunc auctor malesuada et ac mi. Donec non diam a lectus hendrerit aliquet sed ut orci. Suspendisse et facilisis nunc. Fusce dolor eros, suscipit sit amet varius et, iaculis vitae leo. Donec sit amet venenatis massa. Pellentesque consequat laoreet urna sollicitudin volutpat. Integer congue felis a quam pulvinar tristique. Class aptent taciti sociosqu ad litora torquent per conubia nostra, per inceptos himenaeos. Donec fringilla pharetra justo ac tristique. Phasellus pulvinar orci a lorem eleifend, scelerisque ullamcorper purus suscipit. '),
(33, 72, 0, 6, NULL),
(34, 82, 0, 6, 'product configuration magento'),
(35, 100, 0, 6, NULL),
(36, 73, 0, 6, NULL),
(37, 72, 0, 7, NULL),
(38, 82, 0, 7, 'product configuration magento'),
(39, 100, 0, 7, NULL),
(40, 73, 0, 7, NULL),
(41, 72, 0, 8, NULL),
(42, 82, 0, 8, 'product configuration magento'),
(43, 100, 0, 8, NULL),
(44, 73, 0, 8, NULL),
(45, 72, 0, 9, '<p>You won''t know what you like best about the Antonia Racer Tank: soft, stretchy, lightweight fabric? Super-cute colorblocked details? Whatever it is, this piece is sure to quickly move to the top of your workout rotation.</p>\r\n<p>You won''t know what you like best about the Antonia Racer Tank: soft, stretchy, lightweight fabric? Super-cute colorblocked details? Whatever it is, this piece is sure to quickly move to the top of your workout rotation.</p>\r\n<p><span>You won''t know what you like best about the Antonia Racer Tank: soft, stretchy, lightweight fabric? Super-cute colorblocked details? Whatever it is, this piece is sure to quickly move to the top of your workout rotation.</span></p>'),
(46, 82, 0, 9, 'Magento Bundle Product Type'),
(47, 100, 0, 9, NULL),
(48, 73, 0, 9, '<p>You won''t know what you like best about the Antonia Racer Tank: soft, stretchy, lightweight fabric? Super-cute colorblocked details? Whatever it is, this piece is sure to quickly move to the top of your workout rotation.</p>'),
(52, 72, 0, 10, '<p>You won''t know what you like best about the Antonia Racer Tank: soft, stretchy, lightweight fabric? Super-cute colorblocked details? Whatever it is, this piece is sure to quickly move to the top of your workout rotation.</p>\r\n<p><span>You won''t know what you like best about the Antonia Racer Tank: soft, stretchy, lightweight fabric? Super-cute colorblocked details? Whatever it is, this piece is sure to quickly move to the top of your workout rotation.</span></p>\r\n<p><span><span>You won''t know what you like best about the Antonia Racer Tank: soft, stretchy, lightweight fabric? Super-cute colorblocked details? Whatever it is, this piece is sure to quickly move to the top of your workout rotation.</span></span></p>'),
(53, 82, 0, 10, 'Grouped products '),
(54, 100, 0, 10, NULL),
(55, 73, 0, 10, '<p>You won''t know what you like best about the Antonia Racer Tank: soft, stretchy, lightweight fabric? Super-cute colorblocked details? Whatever it is, this piece is sure to quickly move to the top of your workout rotation.</p>'),
(61, 72, 0, 12, '<p>You won''t know what you like best about the Antonia Racer Tank: soft, stretchy, lightweight fabric? Super-cute colorblocked details? Whatever it is, this piece is sure to quickly move to the top of your workout rotation.</p>\r\n<p><span>You won''t know what you like best about the Antonia Racer Tank: soft, stretchy, lightweight fabric? Super-cute colorblocked details? Whatever it is, this piece is sure to quickly move to the top of your workout rotation.</span></p>\r\n<p><span>You won''t know what you like best about the Antonia Racer Tank: soft, stretchy, lightweight fabric? Super-cute colorblocked details? Whatever it is, this piece is sure to quickly move to the top of your workout rotation.</span></p>'),
(62, 82, 0, 12, ' Ariel Roll Sleeve Sweatshirt'),
(63, 100, 0, 12, NULL),
(64, 73, 0, 12, '<p><span>You won''t know what you like best about the Antonia Racer Tank: soft, stretchy, lightweight fabric? Super-cute colorblocked details? Whatever it is, this piece is sure to quickly move to the top of your workout rotation.</span></p>');

-- --------------------------------------------------------

--
-- Table structure for table `catalog_product_entity_tier_price`
--

CREATE TABLE `catalog_product_entity_tier_price` (
  `value_id` int(11) NOT NULL COMMENT 'Value ID',
  `entity_id` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Entity ID',
  `all_groups` smallint(5) UNSIGNED NOT NULL DEFAULT '1' COMMENT 'Is Applicable To All Customer Groups',
  `customer_group_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Customer Group ID',
  `qty` decimal(12,4) NOT NULL DEFAULT '1.0000' COMMENT 'QTY',
  `value` decimal(12,4) NOT NULL DEFAULT '0.0000' COMMENT 'Value',
  `website_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Website ID'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Catalog Product Tier Price Attribute Backend Table';

-- --------------------------------------------------------

--
-- Table structure for table `catalog_product_entity_varchar`
--

CREATE TABLE `catalog_product_entity_varchar` (
  `value_id` int(11) NOT NULL COMMENT 'Value ID',
  `attribute_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Attribute ID',
  `store_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Store ID',
  `entity_id` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Entity ID',
  `value` varchar(255) DEFAULT NULL COMMENT 'Value'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Catalog Product Varchar Attribute Backend Table';

--
-- Dumping data for table `catalog_product_entity_varchar`
--

INSERT INTO `catalog_product_entity_varchar` (`value_id`, `attribute_id`, `store_id`, `entity_id`, `value`) VALUES
(1, 70, 0, 1, 'Ariel Roll Sleeve Sweatshirt'),
(2, 128, 0, 1, '/f/a/fasony100.jpg'),
(3, 84, 0, 1, '/f/a/fasony100.jpg'),
(4, 85, 0, 1, '/f/a/fasony100.jpg'),
(5, 86, 0, 1, '/f/a/fasony100.jpg'),
(6, 115, 0, 1, 'ariel-roll-sleeve-sweatshirt'),
(7, 81, 0, 1, 'Ariel Roll Sleeve Sweatshirt'),
(8, 83, 0, 1, 'Ariel Roll Sleeve Sweatshirt '),
(9, 97, 0, 1, NULL),
(10, 101, 0, 1, NULL),
(11, 103, 0, 1, 'container2'),
(12, 111, 0, 1, NULL),
(13, 106, 0, 1, NULL),
(14, 107, 0, 1, NULL),
(15, 108, 0, 1, NULL),
(16, 130, 0, 1, NULL),
(17, 70, 0, 2, 'Arcadio Gym Short-32-Blue'),
(18, 128, 0, 2, '/f/a/fasony101_3.jpg'),
(19, 84, 0, 2, '/f/a/fasony101_3.jpg'),
(20, 85, 0, 2, '/f/a/fasony101_3.jpg'),
(21, 86, 0, 2, '/f/a/fasony101_3.jpg'),
(22, 115, 0, 2, 'arcadio-gym-short-32-blue'),
(23, 81, 0, 2, 'Arcadio Gym Short-32-Blue'),
(24, 83, 0, 2, 'Arcadio Gym Short-32-Blue '),
(25, 97, 0, 2, NULL),
(26, 101, 0, 2, NULL),
(27, 103, 0, 2, 'container2'),
(28, 111, 0, 2, NULL),
(29, 130, 0, 2, NULL),
(30, 106, 0, 2, NULL),
(31, 107, 0, 2, NULL),
(32, 108, 0, 2, NULL),
(58, 70, 0, 3, 'Atomic Endurance Running Tee'),
(59, 128, 0, 3, '/f/a/fasony107.jpg'),
(60, 84, 0, 3, '/f/a/fasony107.jpg'),
(61, 85, 0, 3, '/f/a/fasony107.jpg'),
(62, 86, 0, 3, '/f/a/fasony107.jpg'),
(63, 115, 0, 3, 'atomic-endurance-running-tee'),
(64, 81, 0, 3, 'Atomic Endurance Running Tee'),
(65, 83, 0, 3, 'Atomic Endurance Running Tee '),
(66, 97, 0, 3, NULL),
(67, 101, 0, 3, NULL),
(68, 103, 0, 3, 'container2'),
(69, 106, 0, 3, NULL),
(70, 107, 0, 3, NULL),
(71, 108, 0, 3, NULL),
(72, 130, 0, 3, NULL),
(73, 70, 0, 4, 'Arcadio Gym Short'),
(74, 128, 0, 4, '/f/a/fasony106.jpg'),
(75, 84, 0, 4, '/f/a/fasony106.jpg'),
(76, 85, 0, 4, '/f/a/fasony106.jpg'),
(77, 86, 0, 4, '/f/a/fasony106.jpg'),
(78, 115, 0, 4, 'arcadio-gym-short'),
(79, 81, 0, 4, 'Arcadio Gym Short'),
(80, 83, 0, 4, 'Arcadio Gym Short '),
(81, 97, 0, 4, NULL),
(82, 101, 0, 4, NULL),
(83, 103, 0, 4, 'container2'),
(84, 106, 0, 4, NULL),
(85, 107, 0, 4, NULL),
(86, 108, 0, 4, NULL),
(87, 130, 0, 4, NULL),
(88, 70, 0, 5, 'product configuration magento'),
(89, 84, 0, 5, '/f/a/fasony105.jpg'),
(90, 85, 0, 5, '/f/a/fasony105.jpg'),
(91, 86, 0, 5, '/f/a/fasony105.jpg'),
(92, 115, 0, 5, 'product-configuration-magento'),
(93, 81, 0, 5, 'product configuration magento'),
(94, 83, 0, 5, 'product configuration magento '),
(95, 97, 0, 5, NULL),
(96, 101, 0, 5, NULL),
(97, 103, 0, 5, 'container2'),
(98, 111, 0, 5, NULL),
(99, 106, 0, 5, NULL),
(100, 107, 0, 5, NULL),
(101, 108, 0, 5, NULL),
(102, 130, 0, 5, NULL),
(103, 70, 0, 6, 'product configuration magento-blue'),
(104, 81, 0, 6, 'product configuration magento'),
(105, 83, 0, 6, 'product configuration magento '),
(106, 118, 0, 6, NULL),
(107, 97, 0, 6, NULL),
(108, 101, 0, 6, NULL),
(109, 103, 0, 6, 'container2'),
(110, 130, 0, 6, NULL),
(111, 84, 0, 6, '/f/a/fasony100_3.jpg'),
(112, 86, 0, 6, '/f/a/fasony100_3.jpg'),
(113, 85, 0, 6, '/f/a/fasony100_3.jpg'),
(114, 115, 0, 6, 'product-configuration-magento-blue'),
(115, 106, 0, 6, NULL),
(116, 107, 0, 6, NULL),
(117, 108, 0, 6, NULL),
(118, 70, 0, 7, 'product configuration magento-pink'),
(119, 81, 0, 7, 'product configuration magento'),
(120, 83, 0, 7, 'product configuration magento '),
(121, 118, 0, 7, NULL),
(122, 97, 0, 7, NULL),
(123, 101, 0, 7, NULL),
(124, 103, 0, 7, 'container2'),
(125, 130, 0, 7, NULL),
(126, 84, 0, 7, '/f/a/fasony106_1.jpg'),
(127, 86, 0, 7, '/f/a/fasony106_1.jpg'),
(128, 85, 0, 7, '/f/a/fasony106_1.jpg'),
(129, 115, 0, 7, 'product-configuration-magento-pink'),
(130, 106, 0, 7, NULL),
(131, 107, 0, 7, NULL),
(132, 108, 0, 7, NULL),
(133, 70, 0, 8, 'product configuration magento-red'),
(134, 81, 0, 8, 'product configuration magento'),
(135, 83, 0, 8, 'product configuration magento '),
(136, 118, 0, 8, NULL),
(137, 97, 0, 8, NULL),
(138, 101, 0, 8, NULL),
(139, 103, 0, 8, 'container2'),
(140, 130, 0, 8, NULL),
(141, 84, 0, 8, '/f/a/fasony101_3_1.jpg'),
(142, 86, 0, 8, '/f/a/fasony101_3_1.jpg'),
(143, 85, 0, 8, '/f/a/fasony101_3_1.jpg'),
(144, 115, 0, 8, 'product-configuration-magento-red'),
(145, 106, 0, 8, NULL),
(146, 107, 0, 8, NULL),
(147, 108, 0, 8, NULL),
(148, 128, 0, 5, NULL),
(149, 70, 0, 9, 'Magento Bundle Product Type'),
(150, 84, 0, 9, '/f/a/fasony104.jpg'),
(151, 85, 0, 9, '/f/a/fasony104.jpg'),
(152, 86, 0, 9, '/f/a/fasony104.jpg'),
(153, 115, 0, 9, 'magento-bundle-product-type'),
(154, 81, 0, 9, 'Magento Bundle Product Type'),
(155, 83, 0, 9, 'Magento Bundle Product Type <p>You won''t know what you like best about the Antonia Racer Tank: soft, stretchy, lightweight fabric? Super-cute colorblocked details? Whatever it is, this piece is sure to quickly move to the top of your workout rotation.</p>'),
(156, 97, 0, 9, NULL),
(157, 101, 0, 9, NULL),
(158, 103, 0, 9, 'container2'),
(159, 111, 0, 9, NULL),
(160, 106, 0, 9, NULL),
(161, 107, 0, 9, NULL),
(162, 108, 0, 9, NULL),
(163, 130, 0, 9, NULL),
(185, 70, 0, 10, 'Magento grouped products type'),
(186, 84, 0, 10, '/f/a/fasony103.jpg'),
(187, 85, 0, 10, '/f/a/fasony103.jpg'),
(188, 86, 0, 10, '/f/a/fasony103.jpg'),
(189, 115, 0, 10, 'grouped-products'),
(190, 81, 0, 10, 'Grouped products '),
(191, 83, 0, 10, 'Grouped products  <p>You won''t know what you like best about the Antonia Racer Tank: soft, stretchy, lightweight fabric? Super-cute colorblocked details? Whatever it is, this piece is sure to quickly move to the top of your workout rotation.</p>\r\n<p><span'),
(192, 97, 0, 10, NULL),
(193, 101, 0, 10, NULL),
(194, 103, 0, 10, 'container2'),
(195, 111, 0, 10, NULL),
(196, 106, 0, 10, NULL),
(197, 107, 0, 10, NULL),
(198, 108, 0, 10, NULL),
(199, 130, 0, 10, NULL),
(223, 70, 0, 12, ' Ariel Roll Sleeve Sweatshirt women'),
(224, 128, 0, 12, '/f/a/fasony102_1.jpg'),
(225, 84, 0, 12, '/f/a/fasony102_1.jpg'),
(226, 85, 0, 12, '/f/a/fasony102_1.jpg'),
(227, 86, 0, 12, '/f/a/fasony102_1.jpg'),
(228, 115, 0, 12, 'ariel-roll-sleeve-sweatshirt-women'),
(229, 81, 0, 12, ' Ariel Roll Sleeve Sweatshirt'),
(230, 83, 0, 12, ' Ariel Roll Sleeve Sweatshirt <p>You won''t know what you like best about the Antonia Racer Tank: soft, stretchy, lightweight fabric? Super-cute colorblocked details? Whatever it is, this piece is sure to quickly move to the top of your workout rotation.</'),
(231, 97, 0, 12, NULL),
(232, 101, 0, 12, NULL),
(233, 103, 0, 12, 'container2'),
(234, 111, 0, 12, NULL),
(235, 106, 0, 12, NULL),
(236, 107, 0, 12, NULL),
(237, 108, 0, 12, NULL),
(238, 130, 0, 12, NULL);

-- --------------------------------------------------------

--
-- Table structure for table `catalog_product_index_eav`
--

CREATE TABLE `catalog_product_index_eav` (
  `entity_id` int(10) UNSIGNED NOT NULL COMMENT 'Entity ID',
  `attribute_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Attribute ID',
  `store_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Store ID',
  `value` int(10) UNSIGNED NOT NULL COMMENT 'Value'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Catalog Product EAV Index Table';

--
-- Dumping data for table `catalog_product_index_eav`
--

INSERT INTO `catalog_product_index_eav` (`entity_id`, `attribute_id`, `store_id`, `value`) VALUES
(5, 90, 1, 4),
(5, 90, 1, 5),
(5, 90, 1, 6),
(5, 90, 2, 4),
(5, 90, 2, 5),
(5, 90, 2, 6),
(9, 90, 1, 4),
(9, 90, 2, 4),
(12, 90, 1, 4),
(12, 90, 2, 4);

-- --------------------------------------------------------

--
-- Table structure for table `catalog_product_index_eav_decimal`
--

CREATE TABLE `catalog_product_index_eav_decimal` (
  `entity_id` int(10) UNSIGNED NOT NULL COMMENT 'Entity ID',
  `attribute_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Attribute ID',
  `store_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Store ID',
  `value` decimal(12,4) NOT NULL COMMENT 'Value'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Catalog Product EAV Decimal Index Table';

-- --------------------------------------------------------

--
-- Table structure for table `catalog_product_index_eav_decimal_idx`
--

CREATE TABLE `catalog_product_index_eav_decimal_idx` (
  `entity_id` int(10) UNSIGNED NOT NULL COMMENT 'Entity ID',
  `attribute_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Attribute ID',
  `store_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Store ID',
  `value` decimal(12,4) NOT NULL COMMENT 'Value'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Catalog Product EAV Decimal Indexer Index Table';

-- --------------------------------------------------------

--
-- Table structure for table `catalog_product_index_eav_decimal_tmp`
--

CREATE TABLE `catalog_product_index_eav_decimal_tmp` (
  `entity_id` int(10) UNSIGNED NOT NULL COMMENT 'Entity ID',
  `attribute_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Attribute ID',
  `store_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Store ID',
  `value` decimal(12,4) NOT NULL COMMENT 'Value'
) ENGINE=MEMORY DEFAULT CHARSET=utf8 COMMENT='Catalog Product EAV Decimal Indexer Temp Table';

-- --------------------------------------------------------

--
-- Table structure for table `catalog_product_index_eav_idx`
--

CREATE TABLE `catalog_product_index_eav_idx` (
  `entity_id` int(10) UNSIGNED NOT NULL COMMENT 'Entity ID',
  `attribute_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Attribute ID',
  `store_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Store ID',
  `value` int(10) UNSIGNED NOT NULL COMMENT 'Value'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Catalog Product EAV Indexer Index Table';

--
-- Dumping data for table `catalog_product_index_eav_idx`
--

INSERT INTO `catalog_product_index_eav_idx` (`entity_id`, `attribute_id`, `store_id`, `value`) VALUES
(5, 90, 1, 4),
(5, 90, 1, 5),
(5, 90, 1, 6),
(5, 90, 2, 4),
(5, 90, 2, 5),
(5, 90, 2, 6),
(9, 90, 1, 4),
(9, 90, 2, 4),
(12, 90, 1, 4),
(12, 90, 2, 4);

-- --------------------------------------------------------

--
-- Table structure for table `catalog_product_index_eav_tmp`
--

CREATE TABLE `catalog_product_index_eav_tmp` (
  `entity_id` int(10) UNSIGNED NOT NULL COMMENT 'Entity ID',
  `attribute_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Attribute ID',
  `store_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Store ID',
  `value` int(10) UNSIGNED NOT NULL COMMENT 'Value'
) ENGINE=MEMORY DEFAULT CHARSET=utf8 COMMENT='Catalog Product EAV Indexer Temp Table';

--
-- Dumping data for table `catalog_product_index_eav_tmp`
--

INSERT INTO `catalog_product_index_eav_tmp` (`entity_id`, `attribute_id`, `store_id`, `value`) VALUES
(9, 90, 1, 4),
(9, 90, 2, 4);

-- --------------------------------------------------------

--
-- Table structure for table `catalog_product_index_price`
--

CREATE TABLE `catalog_product_index_price` (
  `entity_id` int(10) UNSIGNED NOT NULL COMMENT 'Entity ID',
  `customer_group_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Customer Group ID',
  `website_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Website ID',
  `tax_class_id` smallint(5) UNSIGNED DEFAULT '0' COMMENT 'Tax Class ID',
  `price` decimal(12,4) DEFAULT NULL COMMENT 'Price',
  `final_price` decimal(12,4) DEFAULT NULL COMMENT 'Final Price',
  `min_price` decimal(12,4) DEFAULT NULL COMMENT 'Min Price',
  `max_price` decimal(12,4) DEFAULT NULL COMMENT 'Max Price',
  `tier_price` decimal(12,4) DEFAULT NULL COMMENT 'Tier Price'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Catalog Product Price Index Table';

--
-- Dumping data for table `catalog_product_index_price`
--

INSERT INTO `catalog_product_index_price` (`entity_id`, `customer_group_id`, `website_id`, `tax_class_id`, `price`, `final_price`, `min_price`, `max_price`, `tier_price`) VALUES
(1, 0, 1, 0, '150.0000', '150.0000', '150.0000', '150.0000', NULL),
(1, 1, 1, 0, '150.0000', '150.0000', '150.0000', '150.0000', NULL),
(1, 2, 1, 0, '150.0000', '150.0000', '150.0000', '150.0000', NULL),
(1, 3, 1, 0, '150.0000', '150.0000', '150.0000', '150.0000', NULL),
(2, 0, 1, 0, '25.0000', '25.0000', '25.0000', '25.0000', NULL),
(2, 1, 1, 0, '25.0000', '25.0000', '25.0000', '25.0000', NULL),
(2, 2, 1, 0, '25.0000', '25.0000', '25.0000', '25.0000', NULL),
(2, 3, 1, 0, '25.0000', '25.0000', '25.0000', '25.0000', NULL),
(3, 0, 1, 2, '25.0000', '25.0000', '25.0000', '25.0000', NULL),
(3, 1, 1, 2, '25.0000', '25.0000', '25.0000', '25.0000', NULL),
(3, 2, 1, 2, '25.0000', '25.0000', '25.0000', '25.0000', NULL),
(3, 3, 1, 2, '25.0000', '25.0000', '25.0000', '25.0000', NULL),
(4, 0, 1, 0, '24.0000', '24.0000', '24.0000', '24.0000', NULL),
(4, 1, 1, 0, '24.0000', '24.0000', '24.0000', '24.0000', NULL),
(4, 2, 1, 0, '24.0000', '24.0000', '24.0000', '24.0000', NULL),
(4, 3, 1, 0, '24.0000', '24.0000', '24.0000', '24.0000', NULL),
(5, 0, 1, 0, '120.0000', '120.0000', '120.0000', '120.0000', NULL),
(5, 1, 1, 0, '120.0000', '120.0000', '120.0000', '120.0000', NULL),
(5, 2, 1, 0, '120.0000', '120.0000', '120.0000', '120.0000', NULL),
(5, 3, 1, 0, '120.0000', '120.0000', '120.0000', '120.0000', NULL),
(6, 0, 1, 0, '120.0000', '120.0000', '120.0000', '120.0000', NULL),
(6, 1, 1, 0, '120.0000', '120.0000', '120.0000', '120.0000', NULL),
(6, 2, 1, 0, '120.0000', '120.0000', '120.0000', '120.0000', NULL),
(6, 3, 1, 0, '120.0000', '120.0000', '120.0000', '120.0000', NULL),
(7, 0, 1, 0, '120.0000', '120.0000', '120.0000', '120.0000', NULL),
(7, 1, 1, 0, '120.0000', '120.0000', '120.0000', '120.0000', NULL),
(7, 2, 1, 0, '120.0000', '120.0000', '120.0000', '120.0000', NULL),
(7, 3, 1, 0, '120.0000', '120.0000', '120.0000', '120.0000', NULL),
(8, 0, 1, 0, '120.0000', '120.0000', '120.0000', '120.0000', NULL),
(8, 1, 1, 0, '120.0000', '120.0000', '120.0000', '120.0000', NULL),
(8, 2, 1, 0, '120.0000', '120.0000', '120.0000', '120.0000', NULL),
(8, 3, 1, 0, '120.0000', '120.0000', '120.0000', '120.0000', NULL),
(9, 0, 1, 0, '50.0000', '0.0000', '120.0000', '270.0000', NULL),
(9, 1, 1, 0, '50.0000', '0.0000', '120.0000', '270.0000', NULL),
(9, 2, 1, 0, '50.0000', '0.0000', '120.0000', '270.0000', NULL),
(9, 3, 1, 0, '50.0000', '0.0000', '120.0000', '270.0000', NULL),
(10, 0, 1, 0, NULL, NULL, '24.0000', '25.0000', NULL),
(10, 1, 1, 0, NULL, NULL, '24.0000', '25.0000', NULL),
(10, 2, 1, 0, NULL, NULL, '24.0000', '25.0000', NULL),
(10, 3, 1, 0, NULL, NULL, '24.0000', '25.0000', NULL),
(12, 0, 1, 0, '80.0000', '80.0000', '80.0000', '80.0000', NULL),
(12, 1, 1, 0, '80.0000', '80.0000', '80.0000', '80.0000', NULL),
(12, 2, 1, 0, '80.0000', '80.0000', '80.0000', '80.0000', NULL),
(12, 3, 1, 0, '80.0000', '80.0000', '80.0000', '80.0000', NULL);

-- --------------------------------------------------------

--
-- Table structure for table `catalog_product_index_price_bundle_idx`
--

CREATE TABLE `catalog_product_index_price_bundle_idx` (
  `entity_id` int(10) UNSIGNED NOT NULL COMMENT 'Entity Id',
  `customer_group_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Customer Group Id',
  `website_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Website Id',
  `tax_class_id` smallint(5) UNSIGNED DEFAULT '0' COMMENT 'Tax Class Id',
  `price_type` smallint(5) UNSIGNED NOT NULL COMMENT 'Price Type',
  `special_price` decimal(12,4) DEFAULT NULL COMMENT 'Special Price',
  `tier_percent` decimal(12,4) DEFAULT NULL COMMENT 'Tier Percent',
  `orig_price` decimal(12,4) DEFAULT NULL COMMENT 'Orig Price',
  `price` decimal(12,4) DEFAULT NULL COMMENT 'Price',
  `min_price` decimal(12,4) DEFAULT NULL COMMENT 'Min Price',
  `max_price` decimal(12,4) DEFAULT NULL COMMENT 'Max Price',
  `tier_price` decimal(12,4) DEFAULT NULL COMMENT 'Tier Price',
  `base_tier` decimal(12,4) DEFAULT NULL COMMENT 'Base Tier'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Catalog Product Index Price Bundle Idx';

--
-- Dumping data for table `catalog_product_index_price_bundle_idx`
--

INSERT INTO `catalog_product_index_price_bundle_idx` (`entity_id`, `customer_group_id`, `website_id`, `tax_class_id`, `price_type`, `special_price`, `tier_percent`, `orig_price`, `price`, `min_price`, `max_price`, `tier_price`, `base_tier`) VALUES
(9, 0, 1, 0, 0, '0.0000', NULL, '50.0000', '0.0000', '0.0000', '0.0000', NULL, NULL),
(9, 1, 1, 0, 0, '0.0000', NULL, '50.0000', '0.0000', '0.0000', '0.0000', NULL, NULL),
(9, 2, 1, 0, 0, '0.0000', NULL, '50.0000', '0.0000', '0.0000', '0.0000', NULL, NULL),
(9, 3, 1, 0, 0, '0.0000', NULL, '50.0000', '0.0000', '0.0000', '0.0000', NULL, NULL);

-- --------------------------------------------------------

--
-- Table structure for table `catalog_product_index_price_bundle_opt_idx`
--

CREATE TABLE `catalog_product_index_price_bundle_opt_idx` (
  `entity_id` int(10) UNSIGNED NOT NULL COMMENT 'Entity Id',
  `customer_group_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Customer Group Id',
  `website_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Website Id',
  `option_id` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Option Id',
  `min_price` decimal(12,4) DEFAULT NULL COMMENT 'Min Price',
  `alt_price` decimal(12,4) DEFAULT NULL COMMENT 'Alt Price',
  `max_price` decimal(12,4) DEFAULT NULL COMMENT 'Max Price',
  `tier_price` decimal(12,4) DEFAULT NULL COMMENT 'Tier Price',
  `alt_tier_price` decimal(12,4) DEFAULT NULL COMMENT 'Alt Tier Price'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Catalog Product Index Price Bundle Opt Idx';

--
-- Dumping data for table `catalog_product_index_price_bundle_opt_idx`
--

INSERT INTO `catalog_product_index_price_bundle_opt_idx` (`entity_id`, `customer_group_id`, `website_id`, `option_id`, `min_price`, `alt_price`, `max_price`, `tier_price`, `alt_tier_price`) VALUES
(9, 0, 1, 1, '120.0000', '0.0000', '270.0000', NULL, '0.0000'),
(9, 1, 1, 1, '120.0000', '0.0000', '270.0000', NULL, '0.0000'),
(9, 2, 1, 1, '120.0000', '0.0000', '270.0000', NULL, '0.0000'),
(9, 3, 1, 1, '120.0000', '0.0000', '270.0000', NULL, '0.0000');

-- --------------------------------------------------------

--
-- Table structure for table `catalog_product_index_price_bundle_opt_tmp`
--

CREATE TABLE `catalog_product_index_price_bundle_opt_tmp` (
  `entity_id` int(10) UNSIGNED NOT NULL COMMENT 'Entity Id',
  `customer_group_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Customer Group Id',
  `website_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Website Id',
  `option_id` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Option Id',
  `min_price` decimal(12,4) DEFAULT NULL COMMENT 'Min Price',
  `alt_price` decimal(12,4) DEFAULT NULL COMMENT 'Alt Price',
  `max_price` decimal(12,4) DEFAULT NULL COMMENT 'Max Price',
  `tier_price` decimal(12,4) DEFAULT NULL COMMENT 'Tier Price',
  `alt_tier_price` decimal(12,4) DEFAULT NULL COMMENT 'Alt Tier Price'
) ENGINE=MEMORY DEFAULT CHARSET=utf8 COMMENT='Catalog Product Index Price Bundle Opt Tmp';

-- --------------------------------------------------------

--
-- Table structure for table `catalog_product_index_price_bundle_sel_idx`
--

CREATE TABLE `catalog_product_index_price_bundle_sel_idx` (
  `entity_id` int(10) UNSIGNED NOT NULL COMMENT 'Entity Id',
  `customer_group_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Customer Group Id',
  `website_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Website Id',
  `option_id` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Option Id',
  `selection_id` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Selection Id',
  `group_type` smallint(5) UNSIGNED DEFAULT '0' COMMENT 'Group Type',
  `is_required` smallint(5) UNSIGNED DEFAULT '0' COMMENT 'Is Required',
  `price` decimal(12,4) DEFAULT NULL COMMENT 'Price',
  `tier_price` decimal(12,4) DEFAULT NULL COMMENT 'Tier Price'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Catalog Product Index Price Bundle Sel Idx';

--
-- Dumping data for table `catalog_product_index_price_bundle_sel_idx`
--

INSERT INTO `catalog_product_index_price_bundle_sel_idx` (`entity_id`, `customer_group_id`, `website_id`, `option_id`, `selection_id`, `group_type`, `is_required`, `price`, `tier_price`) VALUES
(9, 0, 1, 1, 1, 1, 1, '150.0000', NULL),
(9, 0, 1, 1, 2, 1, 1, '120.0000', NULL),
(9, 1, 1, 1, 1, 1, 1, '150.0000', NULL),
(9, 1, 1, 1, 2, 1, 1, '120.0000', NULL),
(9, 2, 1, 1, 1, 1, 1, '150.0000', NULL),
(9, 2, 1, 1, 2, 1, 1, '120.0000', NULL),
(9, 3, 1, 1, 1, 1, 1, '150.0000', NULL),
(9, 3, 1, 1, 2, 1, 1, '120.0000', NULL);

-- --------------------------------------------------------

--
-- Table structure for table `catalog_product_index_price_bundle_sel_tmp`
--

CREATE TABLE `catalog_product_index_price_bundle_sel_tmp` (
  `entity_id` int(10) UNSIGNED NOT NULL COMMENT 'Entity Id',
  `customer_group_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Customer Group Id',
  `website_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Website Id',
  `option_id` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Option Id',
  `selection_id` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Selection Id',
  `group_type` smallint(5) UNSIGNED DEFAULT '0' COMMENT 'Group Type',
  `is_required` smallint(5) UNSIGNED DEFAULT '0' COMMENT 'Is Required',
  `price` decimal(12,4) DEFAULT NULL COMMENT 'Price',
  `tier_price` decimal(12,4) DEFAULT NULL COMMENT 'Tier Price'
) ENGINE=MEMORY DEFAULT CHARSET=utf8 COMMENT='Catalog Product Index Price Bundle Sel Tmp';

-- --------------------------------------------------------

--
-- Table structure for table `catalog_product_index_price_bundle_tmp`
--

CREATE TABLE `catalog_product_index_price_bundle_tmp` (
  `entity_id` int(10) UNSIGNED NOT NULL COMMENT 'Entity Id',
  `customer_group_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Customer Group Id',
  `website_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Website Id',
  `tax_class_id` smallint(5) UNSIGNED DEFAULT '0' COMMENT 'Tax Class Id',
  `price_type` smallint(5) UNSIGNED NOT NULL COMMENT 'Price Type',
  `special_price` decimal(12,4) DEFAULT NULL COMMENT 'Special Price',
  `tier_percent` decimal(12,4) DEFAULT NULL COMMENT 'Tier Percent',
  `orig_price` decimal(12,4) DEFAULT NULL COMMENT 'Orig Price',
  `price` decimal(12,4) DEFAULT NULL COMMENT 'Price',
  `min_price` decimal(12,4) DEFAULT NULL COMMENT 'Min Price',
  `max_price` decimal(12,4) DEFAULT NULL COMMENT 'Max Price',
  `tier_price` decimal(12,4) DEFAULT NULL COMMENT 'Tier Price',
  `base_tier` decimal(12,4) DEFAULT NULL COMMENT 'Base Tier'
) ENGINE=MEMORY DEFAULT CHARSET=utf8 COMMENT='Catalog Product Index Price Bundle Tmp';

-- --------------------------------------------------------

--
-- Table structure for table `catalog_product_index_price_cfg_opt_agr_idx`
--

CREATE TABLE `catalog_product_index_price_cfg_opt_agr_idx` (
  `parent_id` int(10) UNSIGNED NOT NULL COMMENT 'Parent ID',
  `child_id` int(10) UNSIGNED NOT NULL COMMENT 'Child ID',
  `customer_group_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Customer Group ID',
  `website_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Website ID',
  `price` decimal(12,4) DEFAULT NULL COMMENT 'Price',
  `tier_price` decimal(12,4) DEFAULT NULL COMMENT 'Tier Price'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Catalog Product Price Indexer Config Option Aggregate Index Table';

-- --------------------------------------------------------

--
-- Table structure for table `catalog_product_index_price_cfg_opt_agr_tmp`
--

CREATE TABLE `catalog_product_index_price_cfg_opt_agr_tmp` (
  `parent_id` int(10) UNSIGNED NOT NULL COMMENT 'Parent ID',
  `child_id` int(10) UNSIGNED NOT NULL COMMENT 'Child ID',
  `customer_group_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Customer Group ID',
  `website_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Website ID',
  `price` decimal(12,4) DEFAULT NULL COMMENT 'Price',
  `tier_price` decimal(12,4) DEFAULT NULL COMMENT 'Tier Price'
) ENGINE=MEMORY DEFAULT CHARSET=utf8 COMMENT='Catalog Product Price Indexer Config Option Aggregate Temp Table';

-- --------------------------------------------------------

--
-- Table structure for table `catalog_product_index_price_cfg_opt_idx`
--

CREATE TABLE `catalog_product_index_price_cfg_opt_idx` (
  `entity_id` int(10) UNSIGNED NOT NULL COMMENT 'Entity ID',
  `customer_group_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Customer Group ID',
  `website_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Website ID',
  `min_price` decimal(12,4) DEFAULT NULL COMMENT 'Min Price',
  `max_price` decimal(12,4) DEFAULT NULL COMMENT 'Max Price',
  `tier_price` decimal(12,4) DEFAULT NULL COMMENT 'Tier Price'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Catalog Product Price Indexer Config Option Index Table';

-- --------------------------------------------------------

--
-- Table structure for table `catalog_product_index_price_cfg_opt_tmp`
--

CREATE TABLE `catalog_product_index_price_cfg_opt_tmp` (
  `entity_id` int(10) UNSIGNED NOT NULL COMMENT 'Entity ID',
  `customer_group_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Customer Group ID',
  `website_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Website ID',
  `min_price` decimal(12,4) DEFAULT NULL COMMENT 'Min Price',
  `max_price` decimal(12,4) DEFAULT NULL COMMENT 'Max Price',
  `tier_price` decimal(12,4) DEFAULT NULL COMMENT 'Tier Price'
) ENGINE=MEMORY DEFAULT CHARSET=utf8 COMMENT='Catalog Product Price Indexer Config Option Temp Table';

-- --------------------------------------------------------

--
-- Table structure for table `catalog_product_index_price_downlod_idx`
--

CREATE TABLE `catalog_product_index_price_downlod_idx` (
  `entity_id` int(10) UNSIGNED NOT NULL COMMENT 'Entity ID',
  `customer_group_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Customer Group ID',
  `website_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Website ID',
  `min_price` decimal(12,4) NOT NULL DEFAULT '0.0000' COMMENT 'Minimum price',
  `max_price` decimal(12,4) NOT NULL DEFAULT '0.0000' COMMENT 'Maximum price'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Indexer Table for price of downloadable products';

-- --------------------------------------------------------

--
-- Table structure for table `catalog_product_index_price_downlod_tmp`
--

CREATE TABLE `catalog_product_index_price_downlod_tmp` (
  `entity_id` int(10) UNSIGNED NOT NULL COMMENT 'Entity ID',
  `customer_group_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Customer Group ID',
  `website_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Website ID',
  `min_price` decimal(12,4) NOT NULL DEFAULT '0.0000' COMMENT 'Minimum price',
  `max_price` decimal(12,4) NOT NULL DEFAULT '0.0000' COMMENT 'Maximum price'
) ENGINE=MEMORY DEFAULT CHARSET=utf8 COMMENT='Temporary Indexer Table for price of downloadable products';

-- --------------------------------------------------------

--
-- Table structure for table `catalog_product_index_price_final_idx`
--

CREATE TABLE `catalog_product_index_price_final_idx` (
  `entity_id` int(10) UNSIGNED NOT NULL COMMENT 'Entity ID',
  `customer_group_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Customer Group ID',
  `website_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Website ID',
  `tax_class_id` smallint(5) UNSIGNED DEFAULT '0' COMMENT 'Tax Class ID',
  `orig_price` decimal(12,4) DEFAULT NULL COMMENT 'Original Price',
  `price` decimal(12,4) DEFAULT NULL COMMENT 'Price',
  `min_price` decimal(12,4) DEFAULT NULL COMMENT 'Min Price',
  `max_price` decimal(12,4) DEFAULT NULL COMMENT 'Max Price',
  `tier_price` decimal(12,4) DEFAULT NULL COMMENT 'Tier Price',
  `base_tier` decimal(12,4) DEFAULT NULL COMMENT 'Base Tier'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Catalog Product Price Indexer Final Index Table';

-- --------------------------------------------------------

--
-- Table structure for table `catalog_product_index_price_final_tmp`
--

CREATE TABLE `catalog_product_index_price_final_tmp` (
  `entity_id` int(10) UNSIGNED NOT NULL COMMENT 'Entity ID',
  `customer_group_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Customer Group ID',
  `website_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Website ID',
  `tax_class_id` smallint(5) UNSIGNED DEFAULT '0' COMMENT 'Tax Class ID',
  `orig_price` decimal(12,4) DEFAULT NULL COMMENT 'Original Price',
  `price` decimal(12,4) DEFAULT NULL COMMENT 'Price',
  `min_price` decimal(12,4) DEFAULT NULL COMMENT 'Min Price',
  `max_price` decimal(12,4) DEFAULT NULL COMMENT 'Max Price',
  `tier_price` decimal(12,4) DEFAULT NULL COMMENT 'Tier Price',
  `base_tier` decimal(12,4) DEFAULT NULL COMMENT 'Base Tier'
) ENGINE=MEMORY DEFAULT CHARSET=utf8 COMMENT='Catalog Product Price Indexer Final Temp Table';

-- --------------------------------------------------------

--
-- Table structure for table `catalog_product_index_price_idx`
--

CREATE TABLE `catalog_product_index_price_idx` (
  `entity_id` int(10) UNSIGNED NOT NULL COMMENT 'Entity ID',
  `customer_group_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Customer Group ID',
  `website_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Website ID',
  `tax_class_id` smallint(5) UNSIGNED DEFAULT '0' COMMENT 'Tax Class ID',
  `price` decimal(12,4) DEFAULT NULL COMMENT 'Price',
  `final_price` decimal(12,4) DEFAULT NULL COMMENT 'Final Price',
  `min_price` decimal(12,4) DEFAULT NULL COMMENT 'Min Price',
  `max_price` decimal(12,4) DEFAULT NULL COMMENT 'Max Price',
  `tier_price` decimal(12,4) DEFAULT NULL COMMENT 'Tier Price'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Catalog Product Price Indexer Index Table';

--
-- Dumping data for table `catalog_product_index_price_idx`
--

INSERT INTO `catalog_product_index_price_idx` (`entity_id`, `customer_group_id`, `website_id`, `tax_class_id`, `price`, `final_price`, `min_price`, `max_price`, `tier_price`) VALUES
(1, 0, 1, 0, '150.0000', '150.0000', '150.0000', '150.0000', NULL),
(1, 1, 1, 0, '150.0000', '150.0000', '150.0000', '150.0000', NULL),
(1, 2, 1, 0, '150.0000', '150.0000', '150.0000', '150.0000', NULL),
(1, 3, 1, 0, '150.0000', '150.0000', '150.0000', '150.0000', NULL),
(2, 0, 1, 0, '25.0000', '25.0000', '25.0000', '25.0000', NULL),
(2, 1, 1, 0, '25.0000', '25.0000', '25.0000', '25.0000', NULL),
(2, 2, 1, 0, '25.0000', '25.0000', '25.0000', '25.0000', NULL),
(2, 3, 1, 0, '25.0000', '25.0000', '25.0000', '25.0000', NULL),
(3, 0, 1, 2, '25.0000', '25.0000', '25.0000', '25.0000', NULL),
(3, 1, 1, 2, '25.0000', '25.0000', '25.0000', '25.0000', NULL),
(3, 2, 1, 2, '25.0000', '25.0000', '25.0000', '25.0000', NULL),
(3, 3, 1, 2, '25.0000', '25.0000', '25.0000', '25.0000', NULL),
(4, 0, 1, 0, '24.0000', '24.0000', '24.0000', '24.0000', NULL),
(4, 1, 1, 0, '24.0000', '24.0000', '24.0000', '24.0000', NULL),
(4, 2, 1, 0, '24.0000', '24.0000', '24.0000', '24.0000', NULL),
(4, 3, 1, 0, '24.0000', '24.0000', '24.0000', '24.0000', NULL),
(5, 0, 1, 0, '120.0000', '120.0000', '120.0000', '120.0000', NULL),
(5, 1, 1, 0, '120.0000', '120.0000', '120.0000', '120.0000', NULL),
(5, 2, 1, 0, '120.0000', '120.0000', '120.0000', '120.0000', NULL),
(5, 3, 1, 0, '120.0000', '120.0000', '120.0000', '120.0000', NULL),
(6, 0, 1, 0, '120.0000', '120.0000', '120.0000', '120.0000', NULL),
(6, 1, 1, 0, '120.0000', '120.0000', '120.0000', '120.0000', NULL),
(6, 2, 1, 0, '120.0000', '120.0000', '120.0000', '120.0000', NULL),
(6, 3, 1, 0, '120.0000', '120.0000', '120.0000', '120.0000', NULL),
(7, 0, 1, 0, '120.0000', '120.0000', '120.0000', '120.0000', NULL),
(7, 1, 1, 0, '120.0000', '120.0000', '120.0000', '120.0000', NULL),
(7, 2, 1, 0, '120.0000', '120.0000', '120.0000', '120.0000', NULL),
(7, 3, 1, 0, '120.0000', '120.0000', '120.0000', '120.0000', NULL),
(8, 0, 1, 0, '120.0000', '120.0000', '120.0000', '120.0000', NULL),
(8, 1, 1, 0, '120.0000', '120.0000', '120.0000', '120.0000', NULL),
(8, 2, 1, 0, '120.0000', '120.0000', '120.0000', '120.0000', NULL),
(8, 3, 1, 0, '120.0000', '120.0000', '120.0000', '120.0000', NULL),
(9, 0, 1, 0, '50.0000', '0.0000', '120.0000', '270.0000', NULL),
(9, 1, 1, 0, '50.0000', '0.0000', '120.0000', '270.0000', NULL),
(9, 2, 1, 0, '50.0000', '0.0000', '120.0000', '270.0000', NULL),
(9, 3, 1, 0, '50.0000', '0.0000', '120.0000', '270.0000', NULL),
(10, 0, 1, 0, NULL, NULL, '24.0000', '25.0000', NULL),
(10, 1, 1, 0, NULL, NULL, '24.0000', '25.0000', NULL),
(10, 2, 1, 0, NULL, NULL, '24.0000', '25.0000', NULL),
(10, 3, 1, 0, NULL, NULL, '24.0000', '25.0000', NULL),
(12, 0, 1, 0, '80.0000', '80.0000', '80.0000', '80.0000', NULL),
(12, 1, 1, 0, '80.0000', '80.0000', '80.0000', '80.0000', NULL),
(12, 2, 1, 0, '80.0000', '80.0000', '80.0000', '80.0000', NULL),
(12, 3, 1, 0, '80.0000', '80.0000', '80.0000', '80.0000', NULL);

-- --------------------------------------------------------

--
-- Table structure for table `catalog_product_index_price_opt_agr_idx`
--

CREATE TABLE `catalog_product_index_price_opt_agr_idx` (
  `entity_id` int(10) UNSIGNED NOT NULL COMMENT 'Entity ID',
  `customer_group_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Customer Group ID',
  `website_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Website ID',
  `option_id` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Option ID',
  `min_price` decimal(12,4) DEFAULT NULL COMMENT 'Min Price',
  `max_price` decimal(12,4) DEFAULT NULL COMMENT 'Max Price',
  `tier_price` decimal(12,4) DEFAULT NULL COMMENT 'Tier Price'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Catalog Product Price Indexer Option Aggregate Index Table';

-- --------------------------------------------------------

--
-- Table structure for table `catalog_product_index_price_opt_agr_tmp`
--

CREATE TABLE `catalog_product_index_price_opt_agr_tmp` (
  `entity_id` int(10) UNSIGNED NOT NULL COMMENT 'Entity ID',
  `customer_group_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Customer Group ID',
  `website_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Website ID',
  `option_id` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Option ID',
  `min_price` decimal(12,4) DEFAULT NULL COMMENT 'Min Price',
  `max_price` decimal(12,4) DEFAULT NULL COMMENT 'Max Price',
  `tier_price` decimal(12,4) DEFAULT NULL COMMENT 'Tier Price'
) ENGINE=MEMORY DEFAULT CHARSET=utf8 COMMENT='Catalog Product Price Indexer Option Aggregate Temp Table';

-- --------------------------------------------------------

--
-- Table structure for table `catalog_product_index_price_opt_idx`
--

CREATE TABLE `catalog_product_index_price_opt_idx` (
  `entity_id` int(10) UNSIGNED NOT NULL COMMENT 'Entity ID',
  `customer_group_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Customer Group ID',
  `website_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Website ID',
  `min_price` decimal(12,4) DEFAULT NULL COMMENT 'Min Price',
  `max_price` decimal(12,4) DEFAULT NULL COMMENT 'Max Price',
  `tier_price` decimal(12,4) DEFAULT NULL COMMENT 'Tier Price'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Catalog Product Price Indexer Option Index Table';

-- --------------------------------------------------------

--
-- Table structure for table `catalog_product_index_price_opt_tmp`
--

CREATE TABLE `catalog_product_index_price_opt_tmp` (
  `entity_id` int(10) UNSIGNED NOT NULL COMMENT 'Entity ID',
  `customer_group_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Customer Group ID',
  `website_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Website ID',
  `min_price` decimal(12,4) DEFAULT NULL COMMENT 'Min Price',
  `max_price` decimal(12,4) DEFAULT NULL COMMENT 'Max Price',
  `tier_price` decimal(12,4) DEFAULT NULL COMMENT 'Tier Price'
) ENGINE=MEMORY DEFAULT CHARSET=utf8 COMMENT='Catalog Product Price Indexer Option Temp Table';

-- --------------------------------------------------------

--
-- Table structure for table `catalog_product_index_price_tmp`
--

CREATE TABLE `catalog_product_index_price_tmp` (
  `entity_id` int(10) UNSIGNED NOT NULL COMMENT 'Entity ID',
  `customer_group_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Customer Group ID',
  `website_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Website ID',
  `tax_class_id` smallint(5) UNSIGNED DEFAULT '0' COMMENT 'Tax Class ID',
  `price` decimal(12,4) DEFAULT NULL COMMENT 'Price',
  `final_price` decimal(12,4) DEFAULT NULL COMMENT 'Final Price',
  `min_price` decimal(12,4) DEFAULT NULL COMMENT 'Min Price',
  `max_price` decimal(12,4) DEFAULT NULL COMMENT 'Max Price',
  `tier_price` decimal(12,4) DEFAULT NULL COMMENT 'Tier Price'
) ENGINE=MEMORY DEFAULT CHARSET=utf8 COMMENT='Catalog Product Price Indexer Temp Table';

-- --------------------------------------------------------

--
-- Table structure for table `catalog_product_index_tier_price`
--

CREATE TABLE `catalog_product_index_tier_price` (
  `entity_id` int(10) UNSIGNED NOT NULL COMMENT 'Entity ID',
  `customer_group_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Customer Group ID',
  `website_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Website ID',
  `min_price` decimal(12,4) DEFAULT NULL COMMENT 'Min Price'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Catalog Product Tier Price Index Table';

-- --------------------------------------------------------

--
-- Table structure for table `catalog_product_index_website`
--

CREATE TABLE `catalog_product_index_website` (
  `website_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Website ID',
  `website_date` date DEFAULT NULL COMMENT 'Website Date',
  `rate` float DEFAULT '1' COMMENT 'Rate'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Catalog Product Website Index Table';

--
-- Dumping data for table `catalog_product_index_website`
--

INSERT INTO `catalog_product_index_website` (`website_id`, `website_date`, `rate`) VALUES
(1, '2016-04-29', 1);

-- --------------------------------------------------------

--
-- Table structure for table `catalog_product_link`
--

CREATE TABLE `catalog_product_link` (
  `link_id` int(10) UNSIGNED NOT NULL COMMENT 'Link ID',
  `product_id` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Product ID',
  `linked_product_id` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Linked Product ID',
  `link_type_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Link Type ID'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Catalog Product To Product Linkage Table';

--
-- Dumping data for table `catalog_product_link`
--

INSERT INTO `catalog_product_link` (`link_id`, `product_id`, `linked_product_id`, `link_type_id`) VALUES
(1, 4, 1, 1),
(2, 4, 2, 1),
(3, 4, 3, 1),
(4, 10, 3, 3),
(5, 10, 4, 3),
(6, 1, 9, 5),
(7, 1, 10, 5),
(8, 1, 12, 5);

-- --------------------------------------------------------

--
-- Table structure for table `catalog_product_link_attribute`
--

CREATE TABLE `catalog_product_link_attribute` (
  `product_link_attribute_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Product Link Attribute ID',
  `link_type_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Link Type ID',
  `product_link_attribute_code` varchar(32) DEFAULT NULL COMMENT 'Product Link Attribute Code',
  `data_type` varchar(32) DEFAULT NULL COMMENT 'Data Type'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Catalog Product Link Attribute Table';

--
-- Dumping data for table `catalog_product_link_attribute`
--

INSERT INTO `catalog_product_link_attribute` (`product_link_attribute_id`, `link_type_id`, `product_link_attribute_code`, `data_type`) VALUES
(1, 1, 'position', 'int'),
(2, 4, 'position', 'int'),
(3, 5, 'position', 'int'),
(4, 3, 'position', 'int'),
(5, 3, 'qty', 'decimal');

-- --------------------------------------------------------

--
-- Table structure for table `catalog_product_link_attribute_decimal`
--

CREATE TABLE `catalog_product_link_attribute_decimal` (
  `value_id` int(10) UNSIGNED NOT NULL COMMENT 'Value ID',
  `product_link_attribute_id` smallint(5) UNSIGNED DEFAULT NULL COMMENT 'Product Link Attribute ID',
  `link_id` int(10) UNSIGNED NOT NULL COMMENT 'Link ID',
  `value` decimal(12,4) NOT NULL DEFAULT '0.0000' COMMENT 'Value'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Catalog Product Link Decimal Attribute Table';

--
-- Dumping data for table `catalog_product_link_attribute_decimal`
--

INSERT INTO `catalog_product_link_attribute_decimal` (`value_id`, `product_link_attribute_id`, `link_id`, `value`) VALUES
(1, 5, 4, '0.0000'),
(2, 5, 5, '0.0000');

-- --------------------------------------------------------

--
-- Table structure for table `catalog_product_link_attribute_int`
--

CREATE TABLE `catalog_product_link_attribute_int` (
  `value_id` int(10) UNSIGNED NOT NULL COMMENT 'Value ID',
  `product_link_attribute_id` smallint(5) UNSIGNED DEFAULT NULL COMMENT 'Product Link Attribute ID',
  `link_id` int(10) UNSIGNED NOT NULL COMMENT 'Link ID',
  `value` int(11) NOT NULL DEFAULT '0' COMMENT 'Value'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Catalog Product Link Integer Attribute Table';

--
-- Dumping data for table `catalog_product_link_attribute_int`
--

INSERT INTO `catalog_product_link_attribute_int` (`value_id`, `product_link_attribute_id`, `link_id`, `value`) VALUES
(1, 1, 1, 0),
(2, 1, 2, 0),
(3, 1, 3, 0),
(4, 4, 4, 1),
(5, 4, 5, 2),
(6, 3, 6, 0),
(7, 3, 7, 0),
(8, 3, 8, 0);

-- --------------------------------------------------------

--
-- Table structure for table `catalog_product_link_attribute_varchar`
--

CREATE TABLE `catalog_product_link_attribute_varchar` (
  `value_id` int(10) UNSIGNED NOT NULL COMMENT 'Value ID',
  `product_link_attribute_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Product Link Attribute ID',
  `link_id` int(10) UNSIGNED NOT NULL COMMENT 'Link ID',
  `value` varchar(255) DEFAULT NULL COMMENT 'Value'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Catalog Product Link Varchar Attribute Table';

-- --------------------------------------------------------

--
-- Table structure for table `catalog_product_link_type`
--

CREATE TABLE `catalog_product_link_type` (
  `link_type_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Link Type ID',
  `code` varchar(32) DEFAULT NULL COMMENT 'Code'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Catalog Product Link Type Table';

--
-- Dumping data for table `catalog_product_link_type`
--

INSERT INTO `catalog_product_link_type` (`link_type_id`, `code`) VALUES
(1, 'relation'),
(3, 'super'),
(4, 'up_sell'),
(5, 'cross_sell');

-- --------------------------------------------------------

--
-- Table structure for table `catalog_product_option`
--

CREATE TABLE `catalog_product_option` (
  `option_id` int(10) UNSIGNED NOT NULL COMMENT 'Option ID',
  `product_id` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Product ID',
  `type` varchar(50) DEFAULT NULL COMMENT 'Type',
  `is_require` smallint(6) NOT NULL DEFAULT '1' COMMENT 'Is Required',
  `sku` varchar(64) DEFAULT NULL COMMENT 'SKU',
  `max_characters` int(10) UNSIGNED DEFAULT NULL COMMENT 'Max Characters',
  `file_extension` varchar(50) DEFAULT NULL COMMENT 'File Extension',
  `image_size_x` smallint(5) UNSIGNED DEFAULT NULL COMMENT 'Image Size X',
  `image_size_y` smallint(5) UNSIGNED DEFAULT NULL COMMENT 'Image Size Y',
  `sort_order` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Sort Order'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Catalog Product Option Table';

-- --------------------------------------------------------

--
-- Table structure for table `catalog_product_option_price`
--

CREATE TABLE `catalog_product_option_price` (
  `option_price_id` int(10) UNSIGNED NOT NULL COMMENT 'Option Price ID',
  `option_id` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Option ID',
  `store_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Store ID',
  `price` decimal(12,4) NOT NULL DEFAULT '0.0000' COMMENT 'Price',
  `price_type` varchar(7) NOT NULL DEFAULT 'fixed' COMMENT 'Price Type'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Catalog Product Option Price Table';

-- --------------------------------------------------------

--
-- Table structure for table `catalog_product_option_title`
--

CREATE TABLE `catalog_product_option_title` (
  `option_title_id` int(10) UNSIGNED NOT NULL COMMENT 'Option Title ID',
  `option_id` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Option ID',
  `store_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Store ID',
  `title` varchar(255) DEFAULT NULL COMMENT 'Title'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Catalog Product Option Title Table';

-- --------------------------------------------------------

--
-- Table structure for table `catalog_product_option_type_price`
--

CREATE TABLE `catalog_product_option_type_price` (
  `option_type_price_id` int(10) UNSIGNED NOT NULL COMMENT 'Option Type Price ID',
  `option_type_id` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Option Type ID',
  `store_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Store ID',
  `price` decimal(12,4) NOT NULL DEFAULT '0.0000' COMMENT 'Price',
  `price_type` varchar(7) NOT NULL DEFAULT 'fixed' COMMENT 'Price Type'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Catalog Product Option Type Price Table';

-- --------------------------------------------------------

--
-- Table structure for table `catalog_product_option_type_title`
--

CREATE TABLE `catalog_product_option_type_title` (
  `option_type_title_id` int(10) UNSIGNED NOT NULL COMMENT 'Option Type Title ID',
  `option_type_id` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Option Type ID',
  `store_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Store ID',
  `title` varchar(255) DEFAULT NULL COMMENT 'Title'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Catalog Product Option Type Title Table';

-- --------------------------------------------------------

--
-- Table structure for table `catalog_product_option_type_value`
--

CREATE TABLE `catalog_product_option_type_value` (
  `option_type_id` int(10) UNSIGNED NOT NULL COMMENT 'Option Type ID',
  `option_id` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Option ID',
  `sku` varchar(64) DEFAULT NULL COMMENT 'SKU',
  `sort_order` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Sort Order'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Catalog Product Option Type Value Table';

-- --------------------------------------------------------

--
-- Table structure for table `catalog_product_relation`
--

CREATE TABLE `catalog_product_relation` (
  `parent_id` int(10) UNSIGNED NOT NULL COMMENT 'Parent ID',
  `child_id` int(10) UNSIGNED NOT NULL COMMENT 'Child ID'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Catalog Product Relation Table';

--
-- Dumping data for table `catalog_product_relation`
--

INSERT INTO `catalog_product_relation` (`parent_id`, `child_id`) VALUES
(5, 6),
(5, 7),
(5, 8),
(9, 1),
(9, 6),
(10, 3),
(10, 4);

-- --------------------------------------------------------

--
-- Table structure for table `catalog_product_super_attribute`
--

CREATE TABLE `catalog_product_super_attribute` (
  `product_super_attribute_id` int(10) UNSIGNED NOT NULL COMMENT 'Product Super Attribute ID',
  `product_id` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Product ID',
  `attribute_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Attribute ID',
  `position` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Position'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Catalog Product Super Attribute Table';

--
-- Dumping data for table `catalog_product_super_attribute`
--

INSERT INTO `catalog_product_super_attribute` (`product_super_attribute_id`, `product_id`, `attribute_id`, `position`) VALUES
(1, 5, 90, 0);

-- --------------------------------------------------------

--
-- Table structure for table `catalog_product_super_attribute_label`
--

CREATE TABLE `catalog_product_super_attribute_label` (
  `value_id` int(10) UNSIGNED NOT NULL COMMENT 'Value ID',
  `product_super_attribute_id` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Product Super Attribute ID',
  `store_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Store ID',
  `use_default` smallint(5) UNSIGNED DEFAULT '0' COMMENT 'Use Default Value',
  `value` varchar(255) DEFAULT NULL COMMENT 'Value'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Catalog Product Super Attribute Label Table';

--
-- Dumping data for table `catalog_product_super_attribute_label`
--

INSERT INTO `catalog_product_super_attribute_label` (`value_id`, `product_super_attribute_id`, `store_id`, `use_default`, `value`) VALUES
(1, 1, 0, 0, 'Color'),
(2, 1, 1, 0, 'Color');

-- --------------------------------------------------------

--
-- Table structure for table `catalog_product_super_link`
--

CREATE TABLE `catalog_product_super_link` (
  `link_id` int(10) UNSIGNED NOT NULL COMMENT 'Link ID',
  `product_id` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Product ID',
  `parent_id` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Parent ID'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Catalog Product Super Link Table';

--
-- Dumping data for table `catalog_product_super_link`
--

INSERT INTO `catalog_product_super_link` (`link_id`, `product_id`, `parent_id`) VALUES
(1, 6, 5),
(2, 7, 5),
(3, 8, 5);

-- --------------------------------------------------------

--
-- Table structure for table `catalog_product_website`
--

CREATE TABLE `catalog_product_website` (
  `product_id` int(10) UNSIGNED NOT NULL COMMENT 'Product ID',
  `website_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Website ID'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Catalog Product To Website Linkage Table';

--
-- Dumping data for table `catalog_product_website`
--

INSERT INTO `catalog_product_website` (`product_id`, `website_id`) VALUES
(1, 1),
(2, 1),
(3, 1),
(4, 1),
(5, 1),
(6, 1),
(7, 1),
(8, 1),
(9, 1),
(10, 1),
(12, 1);

-- --------------------------------------------------------

--
-- Table structure for table `catalog_url_rewrite_product_category`
--

CREATE TABLE `catalog_url_rewrite_product_category` (
  `url_rewrite_id` int(10) UNSIGNED NOT NULL COMMENT 'url_rewrite_id',
  `category_id` int(10) UNSIGNED NOT NULL COMMENT 'category_id',
  `product_id` int(10) UNSIGNED NOT NULL COMMENT 'product_id'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='url_rewrite_relation';

--
-- Dumping data for table `catalog_url_rewrite_product_category`
--

INSERT INTO `catalog_url_rewrite_product_category` (`url_rewrite_id`, `category_id`, `product_id`) VALUES
(22, 3, 1),
(23, 4, 1),
(24, 5, 1),
(26, 3, 1),
(27, 4, 1),
(28, 5, 1),
(32, 3, 2),
(33, 4, 2),
(34, 5, 2),
(36, 3, 2),
(37, 4, 2),
(38, 5, 2),
(40, 3, 3),
(41, 4, 3),
(42, 5, 3),
(44, 3, 3),
(45, 4, 3),
(46, 5, 3),
(48, 3, 4),
(49, 4, 4),
(50, 5, 4),
(52, 3, 4),
(53, 4, 4),
(54, 5, 4),
(58, 5, 5),
(62, 5, 5),
(57, 4, 5),
(61, 4, 5),
(56, 3, 5),
(60, 3, 5),
(76, 5, 9),
(80, 5, 9),
(75, 4, 9),
(79, 4, 9),
(74, 3, 9),
(78, 3, 9),
(94, 5, 12),
(98, 5, 12),
(93, 4, 12),
(97, 4, 12),
(92, 3, 12),
(96, 3, 12);

-- --------------------------------------------------------

--
-- Table structure for table `checkout_agreement`
--

CREATE TABLE `checkout_agreement` (
  `agreement_id` int(10) UNSIGNED NOT NULL COMMENT 'Agreement Id',
  `name` varchar(255) DEFAULT NULL COMMENT 'Name',
  `content` text COMMENT 'Content',
  `content_height` varchar(25) DEFAULT NULL COMMENT 'Content Height',
  `checkbox_text` text COMMENT 'Checkbox Text',
  `is_active` smallint(6) NOT NULL DEFAULT '0' COMMENT 'Is Active',
  `is_html` smallint(6) NOT NULL DEFAULT '0' COMMENT 'Is Html',
  `mode` smallint(6) NOT NULL DEFAULT '0' COMMENT 'Applied mode'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Checkout Agreement';

-- --------------------------------------------------------

--
-- Table structure for table `checkout_agreement_store`
--

CREATE TABLE `checkout_agreement_store` (
  `agreement_id` int(10) UNSIGNED NOT NULL COMMENT 'Agreement Id',
  `store_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Store Id'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Checkout Agreement Store';

-- --------------------------------------------------------

--
-- Table structure for table `cms_block`
--

CREATE TABLE `cms_block` (
  `block_id` smallint(6) NOT NULL COMMENT 'Block ID',
  `title` varchar(255) NOT NULL COMMENT 'Block Title',
  `identifier` varchar(255) NOT NULL COMMENT 'Block String Identifier',
  `content` mediumtext COMMENT 'Block Content',
  `creation_time` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT 'Block Creation Time',
  `update_time` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP COMMENT 'Block Modification Time',
  `is_active` smallint(6) NOT NULL DEFAULT '1' COMMENT 'Is Block Active'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='CMS Block Table';

--
-- Dumping data for table `cms_block`
--

INSERT INTO `cms_block` (`block_id`, `title`, `identifier`, `content`, `creation_time`, `update_time`, `is_active`) VALUES
(1, 'Fasony - MenuTop', 'fasony-menutop', '<div class="ves-megamenu-custom">\r\n	<ul class="ves-megamenu ves-horizontal">\r\n		<li class="nav-item level0">\r\n			<a class=" nav-anchor" target="_self" href="{{store url=''#''}}">\r\n				<span>Desktops</span>\r\n			</a>\r\n		</li>\r\n\r\n		<li class="nav-item level0">\r\n			<a class=" nav-anchor" target="_self" href="{{store url=''#''}}">\r\n				<span>Shop</span>\r\n			</a>\r\n		</li>\r\n\r\n		<li class="nav-item level0">\r\n			<a class=" nav-anchor" target="_self" href="{{store url=''#''}}">\r\n				<span>Pages</span>\r\n			</a>\r\n		</li>\r\n\r\n		<li class="nav-item level0">\r\n			<a class=" nav-anchor" target="_self" href="{{store url=''#''}}">\r\n				<span>Featureds</span>\r\n			</a>\r\n		</li>\r\n\r\n		<li class="nav-item level0">\r\n			<a class=" nav-anchor" target="_self" href="{{store url=''#''}}">\r\n				<span>Blog</span>\r\n			</a>\r\n		</li>\r\n\r\n	</ul>\r\n</div>', '2016-04-12 15:17:34', '2016-04-15 09:40:15', 1),
(2, 'Fasony - Slideshow - Banner', 'fasony-slideshow-banner', '<div id="owl-demo2" class="owl-carousel owl-theme">         \r\n	<div class="item"> \r\n		<div class="ves-slider">\r\n			<div class="text-content">\r\n				<h2> Fresh burst of color <br/> New Tartine Collection </h2>\r\n				<p> You see that bamboo behind me though, you see that bamboo? Ain’t nothin’ like bamboo. Bless up.</p>\r\n				<a href="#"> learn more </a>\r\n				<a href="#" class="primary"> shop collection </a>\r\n			</div>\r\n			<img src="{{media url="wysiwyg/fasony/home01/slide02.jpg"}}" alt="" class="img-responsive">\r\n		</div>\r\n	</div>\r\n	<div class="item"> \r\n		<div class="ves-slider">\r\n			<div class="text-content position-02">\r\n				<h2> Fresh burst of color <br/> New Tartine Collection </h2>\r\n				<p> You see that bamboo behind me though, you see that bamboo? Ain’t nothin’ like bamboo. Bless up.</p>\r\n				<a href="#"> learn more </a>\r\n				<a href="#" class="primary"> shop collection </a>\r\n			</div>\r\n			<img src="{{media url="wysiwyg/fasony/home01/slide01.jpg"}}" alt="" class="img-responsive">\r\n		</div>\r\n	</div>\r\n</div>\r\n<div class="owl-controls">\r\n	<div class="owl-nav">\r\n		<div class="owl-demo-prev"><i class="fa fa-angle-left"> </i></div>\r\n		<div class="owl-demo-next"><i class="fa fa-angle-right"> </i></div>\r\n	</div>\r\n</div>\r\n<script type="text/javascript">\r\n	require([''jquery'',''owl.carousel/owl.carousel.min''],function(){\r\n		jQuery(document).ready(function() {\r\n			jQuery("#owl-demo2").owlCarousel({\r\n				loop:true,\r\n				margin:10,\r\n				responsiveClass:true,\r\n				dots: true,\r\n				nav: false,\r\n				responsive:{\r\n					0:{\r\n						items:1\r\n					},\r\n					480:{\r\n						items:1\r\n					},\r\n					768:{\r\n						items:1\r\n					},\r\n					1000:{\r\n						items:1\r\n					}\r\n				}\r\n			});\r\n			jQuery(".owl-demo-prev").click(function () {\r\n				jQuery("#owl-demo2").trigger(''prev.owl.carousel'');\r\n			});\r\n			jQuery(".owl-demo-next").click(function () {\r\n				jQuery("#owl-demo2").trigger(''next.owl.carousel'');\r\n			});\r\n		});\r\n	});\r\n</script>', '2016-04-12 15:18:33', '2016-04-18 04:54:35', 1),
(3, 'Fasony - Showcase - Category', 'fasony-showcase-category', '<div class="row">\r\n	<div class="col-lg-3 col-md-3 col-sm-6 col-xs-6">\r\n		<div class="showcase">\r\n			<div class="text-content">\r\n				<h2> Women </h2>\r\n				<p> it on you how you want to live you life. Everyone has a choise.</p>\r\n				<a href="#"> view more </a>\r\n			</div>\r\n			<img src="{{media url="wysiwyg/fasony/home01/banner01.jpg"}}" alt="" class="img-responsive">\r\n		</div>\r\n	</div>\r\n	<div class="col-lg-3 col-md-3 col-sm-6 col-xs-6">\r\n		<div class="showcase">\r\n			<div class="text-content">\r\n				<h2> Women Fashion</h2>\r\n				<p> it on you how you want to live you life. Everyone has a choise.</p>\r\n				<a href="#"> view more </a>\r\n			</div>\r\n			<img src="{{media url="wysiwyg/fasony/home01/banner02.jpg"}}" alt="" class="img-responsive">\r\n		</div>\r\n	</div>\r\n	<div class="col-lg-6 col-md-6 col-sm-12 col-xs-12">\r\n		<div class="showcase">\r\n			<div class="text-content">\r\n				<h2> Women Clothes </h2>\r\n				<p> it on you how you want to live you life. Everyone has a choise.</p>\r\n				<a href="#"> view more </a>\r\n			</div>\r\n			<img src="{{media url="wysiwyg/fasony/home01/banner03.jpg"}}" alt="" class="img-responsive">\r\n		</div>\r\n	</div>\r\n</div>\r\n\r\n<div class="row">\r\n	<div class="col-lg-6 col-md-6 col-sm-12 col-xs-12">\r\n		<div class="showcase bg-custom ">\r\n			<div class="text-content">\r\n				<h2> Men Clothing </h2>\r\n				<p> it on you how you want to live you life. Everyone has a choise.</p>\r\n				<a href="#"> view more </a>\r\n			</div>\r\n			<img src="{{media url="wysiwyg/fasony/home01/banner04.jpg"}}" alt="" class="img-responsive">\r\n		</div>\r\n	</div>\r\n	<div class="col-lg-3 col-md-3 col-sm-6 col-xs-6">\r\n		<div class="showcase bg-custom ">\r\n			<div class="text-content">\r\n				<h2> Men Fashion </h2>\r\n				<p> it on you how you want to live you life. Everyone has a choise.</p>\r\n				<a href="#"> view more </a>\r\n			</div>\r\n			<img src="{{media url="wysiwyg/fasony/home01/banner05.jpg"}}" alt="" class="img-responsive">\r\n		</div>\r\n	</div>\r\n	<div class="col-lg-3 col-md-3 col-sm-6 col-xs-6">\r\n		<div class="showcase bg-custom ">\r\n			<div class="text-content">\r\n				<h2> Accessories </h2>\r\n				<p> it on you how you want to live you life. Everyone has a choise.</p>\r\n				<a href="#"> view more </a>\r\n			</div>\r\n			<img src="{{media url="wysiwyg/fasony/home01/banner06.jpg"}}" alt="" class="img-responsive">\r\n		</div>\r\n	</div>\r\n</div>', '2016-04-12 15:19:37', '2016-04-18 09:22:21', 1),
(4, 'Fasony - NewProducts', 'fasony-newproducts', '<p>{{widget type="Magento\\Catalog\\Block\\Product\\Widget\\NewWidget" display_type="all_products" products_count="8" template="product/widget/new/content/new_grid.phtml"}}</p>', '2016-04-12 15:20:55', '2016-04-15 10:11:47', 1),
(5, 'Fasony - Ourservice', 'fasony-ourservice', '<div class="row">\r\n	<div class="col-lg-4 col-md-4 col-sm-12 col-xs-12">\r\n		<div class="static-block">\r\n			<span class="fa fa-refresh"> </span>\r\n			<h2> Money Back Guarantee! </h2>\r\n			<p> we free 30 days 100% money back & return </p>\r\n		</div>\r\n	</div>\r\n\r\n	<div class="col-lg-4 col-md-4 col-sm-12 col-xs-12">\r\n		<div class="static-block bg-color">\r\n			<span class="fa fa-plane"> </span>\r\n			<h2> Free shipping  world wide</h2>\r\n			<p> Free shipping on all order over $99.00</p>\r\n		</div>\r\n	</div>\r\n\r\n	<div class="col-lg-4 col-md-4 col-sm-12 col-xs-12">\r\n		<div class="static-block">\r\n			<span class="fa fa-life-ring"> </span>\r\n			<h2> Online support 24/7 </h2>\r\n			<p> we are here to  make your day. Lets talk! </p>\r\n		</div>\r\n	</div>\r\n</div>', '2016-04-12 15:21:46', '2016-04-18 08:10:38', 1),
(6, 'Fasony - Testominial', 'fasony-testominial', '<div class="container">\r\n	<div class="block ves-testominial">\r\n		<div class="block-title"> <strong>Testimonial</strong> </div>\r\n\r\n		<div id="owl-demo1" class="owl-carousel owl-theme">         \r\n			<div class="item"> \r\n				<div class="testominial">\r\n					<p> There are many variations of passages of Lorem Ipsum available, but the majority have suffered alteration in some form, by injected humour, or randomised words which don''t look  </p>\r\n					<h3> _Masum Rana_</h3>\r\n				</div>\r\n			</div>\r\n\r\n			<div class="item"> \r\n				<div class="testominial">\r\n					<p> There are many variations of passages of Lorem Ipsum available, but the majority have suffered alteration in some form, by injected humour, or randomised words which don''t look  </p>\r\n					<h3> _Masum Rana_</h3>\r\n				</div>\r\n			</div>\r\n\r\n			<div class="item"> \r\n				<div class="testominial">\r\n					<p> There are many variations of passages of Lorem Ipsum available, but the majority have suffered alteration in some form, by injected humour, or randomised words which don''t look  </p>\r\n					<h3> _Masum Rana_</h3>\r\n				</div>\r\n			</div>\r\n		</div>\r\n		<div class="owl-controls">\r\n			<div class="owl-nav">\r\n				<div class="owl-demo-prev2 left"><i class="fa fa-angle-left"> </i></div>\r\n				<div class="owl-demo-next2 right"><i class="fa fa-angle-right"> </i></div>\r\n			</div>\r\n		</div>\r\n		<script type="text/javascript">\r\n			require([''jquery'',''owl.carousel/owl.carousel.min''],function(){\r\n				jQuery(document).ready(function() {\r\n					jQuery("#owl-demo1").owlCarousel({\r\n						loop:true,\r\n						margin:10,\r\n						responsiveClass:true,\r\n						dots:false,\r\n						nav: false,\r\n						responsive:{\r\n							0:{\r\n								items:1\r\n							},\r\n							480:{\r\n								items:1\r\n							},\r\n							768:{\r\n								items:1\r\n							},\r\n							1000:{\r\n								items:1\r\n							}\r\n						}\r\n					});\r\n					jQuery(".owl-demo-prev2").click(function () {\r\n						jQuery("#owl-demo1").trigger(''prev.owl.carousel'');\r\n					});\r\n					jQuery(".owl-demo-next2").click(function () {\r\n						jQuery("#owl-demo1").trigger(''next.owl.carousel'');\r\n					});\r\n				});\r\n			});\r\n		</script>\r\n	</div>\r\n</div>', '2016-04-12 15:23:00', '2016-04-29 09:04:00', 1),
(7, 'Fasony - OurBrands', 'fasony-ourbrands', '<div class="container">\r\n	<div id="owl-demo" class="owl-carousel owl-theme">         \r\n		<div class="item"> <img src="{{media url="wysiwyg/fasony/brand/brand01.jpg"}}" alt="" class="img-responsive"> </div>\r\n		<div class="item"> <img src="{{media url="wysiwyg/fasony/brand/brand02.jpg"}}" alt="" class="img-responsive"> </div>\r\n		<div class="item"> <img src="{{media url="wysiwyg/fasony/brand/brand03.jpg"}}" alt="" class="img-responsive"> </div>\r\n		<div class="item"> <img src="{{media url="wysiwyg/fasony/brand/brand04.jpg"}}" alt="" class="img-responsive"> </div>\r\n		<div class="item"> <img src="{{media url="wysiwyg/fasony/brand/brand05.jpg"}}" alt="" class="img-responsive"> </div>\r\n		<div class="item"> <img src="{{media url="wysiwyg/fasony/brand/brand06.jpg"}}" alt="" class="img-responsive"> </div>\r\n		<div class="item"> <img src="{{media url="wysiwyg/fasony/brand/brand01.jpg"}}" alt="" class="img-responsive"> </div>\r\n		<div class="item"> <img src="{{media url="wysiwyg/fasony/brand/brand02.jpg"}}" alt="" class="img-responsive"> </div>\r\n	</div>\r\n\r\n	<div class="owl-controls">\r\n		<div class="owl-nav">\r\n			<div class="owl-demo-prev1 left"><i class="fa fa-angle-left"> </i></div>\r\n			<div class="owl-demo-next1 right"><i class="fa fa-angle-right"> </i></div>\r\n		</div>\r\n	</div>\r\n	<script type="text/javascript">\r\n		require([''jquery'',''owl.carousel/owl.carousel.min''],function(){\r\n			jQuery(document).ready(function() {\r\n				jQuery("#owl-demo").owlCarousel({\r\n					loop:true,\r\n					margin:10,\r\n					responsiveClass:true,\r\n					dots: true,\r\n					nav: false,\r\n					responsive:{\r\n						0:{\r\n							items:1\r\n						},\r\n						480:{\r\n							items:2\r\n						},\r\n						768:{\r\n							items:4\r\n						},\r\n						1000:{\r\n							items:6\r\n						}\r\n					}\r\n				});\r\n				jQuery(".owl-demo-prev1").click(function () {\r\n					jQuery("#owl-demo").trigger(''prev.owl.carousel'');\r\n				});\r\n				jQuery(".owl-demo-next1").click(function () {\r\n					jQuery("#owl-demo").trigger(''next.owl.carousel'');\r\n				});\r\n			});\r\n		});\r\n	</script>\r\n</div>', '2016-04-12 15:24:05', '2016-04-22 09:06:07', 1),
(8, 'Fasony - Footer', 'fasony-footer', '<div class="row custom-footer">\r\n<div class="col-lg-3 col-md-3 col-sm-12 col-xs-12"><!-- Col1  -->\r\n<div class="block">\r\n<div class="block-title"><strong> About Fasony </strong></div>\r\n<div class="block-content ">\r\n<p>You see that bamboo behind me though, you see that bamboo? Ain&rsquo;t nothin&rsquo; like bamboo. Bless up.</p>\r\n<ul class="contacts">\r\n<li><em class="fa fa-map-marker">&nbsp; </em> <span>221b Baker Street - London United Kingdom</span></li>\r\n<li><em class="fa fa-headphones">&nbsp;</em> <span> Telephone: (+0) 012-345-678 Fax: (+0) 012-345-678 </span></li>\r\n<li><em class="fa fa-envelope-o">&nbsp;</em> <span>Email: fasony@123.vn</span></li>\r\n</ul>\r\n</div>\r\n</div>\r\n</div>\r\n<div class="col-lg-6 col-md-6 col-sm-12 col-xs-12">\r\n<div class="row">\r\n<div class="col-lg-4 col-md-4 col-sm-4 col-xs-12"><!-- Col2  -->\r\n<div class="block">\r\n<div class="block-title"><strong>Categories</strong></div>\r\n<div class="block-content">\r\n<ul class="nav-links">\r\n<li><a href="{{store url=''men''}}">Men</a></li>\r\n<li><a href="{{store url=''women''}}">Women</a></li>\r\n<li><a href="{{store url=''accessories''}}">New Blazers</a></li>\r\n<li><a href="{{store url=''men''}}">Accessories</a></li>\r\n<li><a href="{{store url=''women''}}">T-Shirt</a></li>\r\n<li><a href="{{store url=''accessories''}}">Summer Hot</a></li>\r\n</ul>\r\n</div>\r\n</div>\r\n</div>\r\n<div class="col-lg-4 col-md-4 col-sm-4 col-xs-12"><!-- Col3  -->\r\n<div class="block">\r\n<div class="block-title"><strong>Help</strong></div>\r\n<div class="block-content">\r\n<ul class="nav-links">\r\n<li><a href="{{store url=''contact''}}">Help &amp; Contact</a></li>\r\n<li><a href="{{store url=''#''}}">Shipping &amp; taxes</a></li>\r\n<li><a href="{{store url=''#''}}">Return policy</a></li>\r\n<li><a href="{{store url=''#''}}">Affiliates</a></li>\r\n<li><a href="{{store url=''#''}}">Legal Notice</a></li>\r\n</ul>\r\n</div>\r\n</div>\r\n</div>\r\n<div class="col-lg-4 col-md-4 col-sm-4 col-xs-12"><!-- Col4  -->\r\n<div class="block">\r\n<div class="block-title"><strong>Quick Link</strong></div>\r\n<div class="block-content">\r\n<ul class="nav-links">\r\n<li><a href="{{store url=''customer/account/login/''}}">My Acount</a></li>\r\n<li><a href="{{store url=''sales/guest/form/''}}">Order history</a></li>\r\n<li><a href="{{store url=''wishlist''}}">Wishlist</a></li>\r\n<li><a href="{{store url=''#''}}">Returns</a></li>\r\n<li><a href="{{store url=''#''}}">Store Location</a></li>\r\n<li><a href="{{store url=''catalog/seo_sitemap/category/''}}">Site map</a></li>\r\n</ul>\r\n</div>\r\n</div>\r\n</div>\r\n</div>\r\n</div>\r\n<div class="col-lg-3 col-md-3 col-sm-12 col-xs-12"><!-- Col5-->\r\n<div>{{block class="Magento\\Newsletter\\Block\\Subscribe" name="form.subscribe" as="subscribe" before="-" template="subscribe.phtml"/}}</div>\r\n<ul class="list-social">\r\n<li class="icon-social"><a href="#"> <em class="fa fa-facebook">&nbsp;</em> </a></li>\r\n<li class="icon-social"><a href="#"> <em class="fa fa-twitter">&nbsp;</em> </a></li>\r\n<li class="icon-social"><a href="#"> <em class="fa fa-google-plus">&nbsp;</em></a></li>\r\n<li class="icon-social"><a href="#"> <em class="fa fa-tumblr">&nbsp;</em> </a></li>\r\n<li class="icon-social"><a href="#"> <em class="fa fa-rss">&nbsp;</em> </a></li>\r\n<li class="icon-social"><a href="#"> <em class="fa fa-skype">&nbsp;</em> </a></li>\r\n</ul>\r\n</div>\r\n</div>', '2016-04-12 15:24:52', '2016-04-29 07:29:25', 1),
(9, 'Fasony Icon pay', 'fasony_icon_pay', '<div> We accept payment through : <img src="{{media url="wysiwyg/fasony/home01/icon_pay.png"}}" alt="" > </div>', '2016-04-18 09:00:13', '2016-04-18 09:01:13', 1),
(10, 'Fasony - Bloglist', 'fasony-blog-list', '<div class="ves-blog">\r\n	<div class="blog-grid">\r\n		<div class="row">\r\n			<div class="col-lg-4 col-md-4 col-sm-4 col-xs-12">\r\n				<div class="ves-post post-item">\r\n					<div class="post-image">\r\n						<a title="Le Creuset Introduces New Ecommerce" href="#">\r\n							<img alt="Le Creuset Introduces New Ecommerce" src="{{media url="wysiwyg/fasony/blogs/blog-01.jpg"}}">\r\n						</a>\r\n					</div>\r\n					<div class="post-meta">\r\n						<div class="post-title">\r\n							<h3><a title="Le Creuset Introduces New Ecommerce" href="{{store url=''blog-detail''}}"> Le Creuset Introduces New Ecommerce</a></h3>\r\n						</div>\r\n						<div class="post-author">\r\n							Posted by: <a title="" href="{{store url=''blog-detail''}}">venusadmin venusadmin</a>\r\n						</div>\r\n						<div class="post-date"> <span>Created on Feb 5, 2016</span></div>\r\n						<div class="post-hits"><span>Read</span> <strong>32</strong> Times</div>\r\n						<div class="post-tag">\r\n							<span>Tags:</span>\r\n							<a href="{{store url=''blog-detail''}}">Enterprise Edition</a>,\r\n							<a href="{{store url=''blog-detail''}}"> Merchants</a>,\r\n							<a href="{{store url=''blog-detail''}}">Partners</a>\r\n						</div>\r\n					</div>\r\n				</div>\r\n			</div>	\r\n\r\n			<div class="col-lg-4 col-md-4 col-sm-4 col-xs-12">\r\n				<div class="ves-post post-item">\r\n					<div class="post-image">\r\n						<a title="Le Creuset Introduces New Ecommerce" href="#">\r\n							<img alt="Le Creuset Introduces New Ecommerce" src="{{media url="wysiwyg/fasony/blogs/blog-02.jpg"}}">\r\n						</a>\r\n					</div>\r\n					<div class="post-meta">\r\n						<div class="post-title">\r\n							<h3><a title="Le Creuset Introduces New Ecommerce" href="{{store url=''blog-detail''}}"> Le Creuset Introduces New Ecommerce</a></h3>\r\n						</div>\r\n						<div class="post-author">\r\n							Posted by: <a title="" href="{{store url=''blog-detail''}}">venusadmin venusadmin</a>\r\n						</div>\r\n						<div class="post-date"> <span>Created on Feb 5, 2016</span></div>\r\n						<div class="post-hits"><span>Read</span> <strong>32</strong> Times</div>\r\n						<div class="post-tag">\r\n							<span>Tags:</span>\r\n							<a href="{{store url=''blog-detail''}}">Enterprise Edition</a>,\r\n							<a href="{{store url=''blog-detail''}}"> Merchants</a>,\r\n							<a href="{{store url=''blog-detail''}}">Partners</a>\r\n						</div>\r\n					</div>\r\n				</div>\r\n			</div>	\r\n\r\n\r\n			<div class="col-lg-4 col-md-4 col-sm-4 col-xs-12">\r\n				<div class="ves-post post-item">\r\n					<div class="post-image">\r\n						<a title="Le Creuset Introduces New Ecommerce" href="#">\r\n							<img alt="Le Creuset Introduces New Ecommerce" src="{{media url="wysiwyg/fasony/blogs/blog-03.jpg"}}">\r\n						</a>\r\n					</div>\r\n					<div class="post-meta">\r\n						<div class="post-title">\r\n							<h3><a title="Le Creuset Introduces New Ecommerce" href="{{store url=''blog-detail''}}"> Le Creuset Introduces New Ecommerce</a></h3>\r\n						</div>\r\n						<div class="post-author">\r\n							Posted by: <a title="" href="{{store url=''blog-detail''}}">venusadmin venusadmin</a>\r\n						</div>\r\n						<div class="post-date"> <span>Created on Feb 5, 2016</span></div>\r\n						<div class="post-hits"><span>Read</span> <strong>32</strong> Times</div>\r\n						<div class="post-tag">\r\n							<span>Tags:</span>\r\n							<a href="{{store url=''blog-detail''}}">Enterprise Edition</a>,\r\n							<a href="{{store url=''blog-detail''}}"> Merchants</a>,\r\n							<a href="{{store url=''blog-detail''}}">Partners</a>\r\n						</div>\r\n					</div>\r\n				</div>\r\n			</div>	\r\n		</div>\r\n\r\n		<div class="row">\r\n			<div class="col-lg-4 col-md-4 col-sm-4 col-xs-12">\r\n				<div class="ves-post post-item">\r\n					<div class="post-image">\r\n						<a title="Le Creuset Introduces New Ecommerce" href="#">\r\n							<img alt="Le Creuset Introduces New Ecommerce" src="{{media url="wysiwyg/fasony/blogs/blog-04.jpg"}}">\r\n						</a>\r\n					</div>\r\n					<div class="post-meta">\r\n						<div class="post-title">\r\n							<h3><a title="Le Creuset Introduces New Ecommerce" href="{{store url=''blog-detail''}}"> Le Creuset Introduces New Ecommerce</a></h3>\r\n						</div>\r\n						<div class="post-author">\r\n							Posted by: <a title="" href="{{store url=''blog-detail''}}">venusadmin venusadmin</a>\r\n						</div>\r\n						<div class="post-date"> <span>Created on Feb 5, 2016</span></div>\r\n						<div class="post-hits"><span>Read</span> <strong>32</strong> Times</div>\r\n						<div class="post-tag">\r\n							<span>Tags:</span>\r\n							<a href="{{store url=''blog-detail''}}">Enterprise Edition</a>,\r\n							<a href="{{store url=''blog-detail''}}"> Merchants</a>,\r\n							<a href="{{store url=''blog-detail''}}">Partners</a>\r\n						</div>\r\n					</div>\r\n				</div>\r\n			</div>	\r\n\r\n			<div class="col-lg-4 col-md-4 col-sm-4 col-xs-12">\r\n				<div class="ves-post post-item">\r\n					<div class="post-image">\r\n						<a title="Le Creuset Introduces New Ecommerce" href="#">\r\n							<img alt="Le Creuset Introduces New Ecommerce" src="{{media url="wysiwyg/fasony/blogs/blog-05.jpg"}}">\r\n						</a>\r\n					</div>\r\n					<div class="post-meta">\r\n						<div class="post-title">\r\n							<h3><a title="Le Creuset Introduces New Ecommerce" href="{{store url=''blog-detail''}}"> Le Creuset Introduces New Ecommerce</a></h3>\r\n						</div>\r\n						<div class="post-author">\r\n							Posted by: <a title="" href="{{store url=''blog-detail''}}">venusadmin venusadmin</a>\r\n						</div>\r\n						<div class="post-date"> <span>Created on Feb 5, 2016</span></div>\r\n						<div class="post-hits"><span>Read</span> <strong>32</strong> Times</div>\r\n						<div class="post-tag">\r\n							<span>Tags:</span>\r\n							<a href="{{store url=''blog-detail''}}">Enterprise Edition</a>,\r\n							<a href="{{store url=''blog-detail''}}"> Merchants</a>,\r\n							<a href="{{store url=''blog-detail''}}">Partners</a>\r\n						</div>\r\n					</div>\r\n				</div>\r\n			</div>	\r\n\r\n\r\n			<div class="col-lg-4 col-md-4 col-sm-4 col-xs-12">\r\n				<div class="ves-post post-item">\r\n					<div class="post-image">\r\n						<a title="Le Creuset Introduces New Ecommerce" href="#">\r\n							<img alt="Le Creuset Introduces New Ecommerce" src="{{media url="wysiwyg/fasony/blogs/blog-06.jpg"}}">\r\n						</a>\r\n					</div>\r\n					<div class="post-meta">\r\n						<div class="post-title">\r\n							<h3><a title="Le Creuset Introduces New Ecommerce" href="{{store url=''blog-detail''}}"> Le Creuset Introduces New Ecommerce</a></h3>\r\n						</div>\r\n						<div class="post-author">\r\n							Posted by: <a title="" href="{{store url=''blog-detail''}}">venusadmin venusadmin</a>\r\n						</div>\r\n						<div class="post-date"> <span>Created on Feb 5, 2016</span></div>\r\n						<div class="post-hits"><span>Read</span> <strong>32</strong> Times</div>\r\n						<div class="post-tag">\r\n							<span>Tags:</span>\r\n							<a href="{{store url=''blog-detail''}}">Enterprise Edition</a>,\r\n							<a href="{{store url=''blog-detail''}}"> Merchants</a>,\r\n							<a href="{{store url=''blog-detail''}}">Partners</a>\r\n						</div>\r\n					</div>\r\n				</div>\r\n			</div>	\r\n		</div>\r\n\r\n\r\n		<div class="row">\r\n			<div class="col-lg-4 col-md-4 col-sm-4 col-xs-12">\r\n				<div class="ves-post post-item">\r\n					<div class="post-image">\r\n						<a title="Le Creuset Introduces New Ecommerce" href="#">\r\n							<img alt="Le Creuset Introduces New Ecommerce" src="{{media url="wysiwyg/fasony/blogs/blog-07.jpg"}}">\r\n						</a>\r\n					</div>\r\n					<div class="post-meta">\r\n						<div class="post-title">\r\n							<h3><a title="Le Creuset Introduces New Ecommerce" href="{{store url=''blog-detail''}}"> Le Creuset Introduces New Ecommerce</a></h3>\r\n						</div>\r\n						<div class="post-author">\r\n							Posted by: <a title="" href="{{store url=''blog-detail''}}">venusadmin venusadmin</a>\r\n						</div>\r\n						<div class="post-date"> <span>Created on Feb 5, 2016</span></div>\r\n						<div class="post-hits"><span>Read</span> <strong>32</strong> Times</div>\r\n						<div class="post-tag">\r\n							<span>Tags:</span>\r\n							<a href="{{store url=''blog-detail''}}">Enterprise Edition</a>,\r\n							<a href="{{store url=''blog-detail''}}"> Merchants</a>,\r\n							<a href="{{store url=''blog-detail''}}">Partners</a>\r\n						</div>\r\n					</div>\r\n				</div>\r\n			</div>	\r\n\r\n			<div class="col-lg-4 col-md-4 col-sm-4 col-xs-12">\r\n				<div class="ves-post post-item">\r\n					<div class="post-image">\r\n						<a title="Le Creuset Introduces New Ecommerce" href="#">\r\n							<img alt="Le Creuset Introduces New Ecommerce" src="{{media url="wysiwyg/fasony/blogs/blog-08.jpg"}}">\r\n						</a>\r\n					</div>\r\n					<div class="post-meta">\r\n						<div class="post-title">\r\n							<h3><a title="Le Creuset Introduces New Ecommerce" href="{{store url=''blog-detail''}}"> Le Creuset Introduces New Ecommerce</a></h3>\r\n						</div>\r\n						<div class="post-author">\r\n							Posted by: <a title="" href="{{store url=''blog-detail''}}">venusadmin venusadmin</a>\r\n						</div>\r\n						<div class="post-date"> <span>Created on Feb 5, 2016</span></div>\r\n						<div class="post-hits"><span>Read</span> <strong>32</strong> Times</div>\r\n						<div class="post-tag">\r\n							<span>Tags:</span>\r\n							<a href="{{store url=''blog-detail''}}">Enterprise Edition</a>,\r\n							<a href="{{store url=''blog-detail''}}"> Merchants</a>,\r\n							<a href="{{store url=''blog-detail''}}">Partners</a>\r\n						</div>\r\n					</div>\r\n				</div>\r\n			</div>	\r\n\r\n\r\n			<div class="col-lg-4 col-md-4 col-sm-4 col-xs-12">\r\n				<div class="ves-post post-item">\r\n					<div class="post-image">\r\n						<a title="Le Creuset Introduces New Ecommerce" href="#">\r\n							<img alt="Le Creuset Introduces New Ecommerce" src="{{media url="wysiwyg/fasony/blogs/blog-09.jpg"}}">\r\n						</a>\r\n					</div>\r\n					<div class="post-meta">\r\n						<div class="post-title">\r\n							<h3><a title="Le Creuset Introduces New Ecommerce" href="{{store url=''blog-detail''}}"> Le Creuset Introduces New Ecommerce</a></h3>\r\n						</div>\r\n						<div class="post-author">\r\n							Posted by: <a title="" href="{{store url=''blog-detail''}}">venusadmin venusadmin</a>\r\n						</div>\r\n						<div class="post-date"> <span>Created on Feb 5, 2016</span></div>\r\n						<div class="post-hits"><span>Read</span> <strong>32</strong> Times</div>\r\n						<div class="post-tag">\r\n							<span>Tags:</span>\r\n							<a href="{{store url=''blog-detail''}}">Enterprise Edition</a>,\r\n							<a href="{{store url=''blog-detail''}}"> Merchants</a>,\r\n							<a href="{{store url=''blog-detail''}}">Partners</a>\r\n						</div>\r\n					</div>\r\n				</div>\r\n			</div>	\r\n		</div>\r\n	</div>\r\n\r\n	<div class="blog-toolbar toolbar">\r\n		<div class="pages">\r\n			<strong id="paging-label" class="label pages-label">Page</strong>\r\n			<ul aria-labelledby="paging-label" class="items pages-items">\r\n				<li class="item current">\r\n					<strong class="page">\r\n						<span class="label">You''re currently reading page</span>\r\n						<span>1</span>\r\n					</strong>\r\n				</li>\r\n				<li class="item">\r\n					<a class="page" href="{{store url=''#''}}">\r\n						<span class="label">Page</span>\r\n						<span>2</span>\r\n					</a>\r\n				</li>\r\n				<li class="item pages-item-next">\r\n					<a title="Next" href="{{store url=''#''}}" class="action  next">\r\n						<span class="label">Page</span>\r\n						<span>Next</span>\r\n					</a>\r\n				</li>\r\n			</ul>\r\n		</div>\r\n	</div>\r\n</div>\r\n', '2016-04-23 04:21:16', '2016-04-29 07:31:53', 1),
(11, 'Fasony - About us', 'fasony-aboutus', '<div class="custom-page">\r\n	<div class="a-center">\r\n		<img alt="About us" src="{{media url="wysiwyg/fasony/about/about-05.jpg"}}">\r\n		<h3>Catering to your requirements, handling your needs with care</h3>\r\n		<p>Our store is more than just another average online retailer. We sell not only top quality products, but give our customers a positive online shopping experience. Forget about struggling to do everything at once: taking care of the family, running your business, walking your dog, cleaning the house, doing the shopping, etc. Purchase the goods you need every day or just like in a few clicks or taps, depending on the device you use to access the Internet. We work to make your life more enjoyable.</p>\r\n	</div>\r\n\r\n	<div class="page-title">\r\n		<h1>Store events</h1>\r\n	</div>\r\n\r\n	<div class="row">\r\n		<div class="col-xs-12 col-sm-4">\r\n			<div class="custom-service a-center">\r\n				<span class="fa fa-search"> &nbsp; </span>\r\n				<h4 class="custom-title">For convenience of choice</h4>\r\n				<p>We think about the convenience of your choice. Our products are supplied with star rating that should help hesitant buyers to take a decision. What’s more, you can search our site if you know exactly what you are looking for or use a bunch of different filters that will considerably save your time and efforts.</p>\r\n			</div>\r\n		</div>\r\n		<div class="col-xs-12 col-sm-4">\r\n			<div class="custom-service a-center">\r\n				<span class="fa fa-car"> &nbsp; </span>\r\n				<h4 class="custom-title">Delivery to all regions</h4>\r\n				<p>We deliver our goods worldwide. No matter where you live, your order will be shipped in time and delivered right to your door or to any other location you have stated. The packages are handled with utmost care, so the ordered products will be handed to you safe and sound, just like you expect them to be. </p>\r\n			</div>\r\n		</div>\r\n		<div class="col-xs-12 col-sm-4">\r\n			<div class="custom-service a-center">\r\n				<span class="fa fa-thumbs-o-up"> &nbsp; </span>\r\n				<h4 class="custom-title3">The highest quality of products</h4>\r\n				<p>We guarantee the highest quality of the products we sell. Several decades of successful operation and millions of happy customers let us feel certain about that. Besides, all items we sell pass thorough quality control, so no characteristics mismatch can escape the eye of our professionals. </p>\r\n			</div>\r\n		</div>\r\n	</div>\r\n\r\n	<div class="page-title">\r\n		<h1>Our team</h1>\r\n	</div>\r\n\r\n	<div class="row">\r\n		<div class="col-xs-12 col-sm-3">\r\n			<div class="team">\r\n				<a title="Robert Johnson" href="#"><img alt="Robert Johnson" src="{{media url="wysiwyg/fasony/about/about-01.jpg"}}"></a>\r\n				<h4><a title="Robert Johnson" href="#">Robert Johnson</a></h4>\r\n				<div class="excerpt">Senior salesman with 15 years of experience. He knows everything about the products he offers.</div>\r\n			</div>\r\n		</div>\r\n		<div class="col-xs-12 col-sm-3">\r\n			<div class="team">\r\n				<a title="JESSICA PRISTON" href="#"><img alt="JESSICA PRISTON" src="{{media url="wysiwyg/fasony/about/about-02.jpg"}}"></a>\r\n				<h4><a title="JESSICA PRISTON" href="#">JESSICA PRISTON</a></h4>\r\n				<div class="excerpt">Mega positive shop assistant always ready to help you make the right choice and charm you with a smile.</div>\r\n			</div>\r\n		</div>\r\n		<div class="col-xs-12 col-sm-3">\r\n			<div class="team">\r\n				<a title="SAM KROMSTAIN" href="#"><img alt="SAM KROMSTAIN" src="{{media url="wysiwyg/fasony/about/about-03.jpg"}}"></a>\r\n				<h4><a title="SAM KROMSTAIN" href="#">SAM KROMSTAIN</a></h4>\r\n				<div class="excerpt">Wholesale manager. Contact him if you want to buy a batch of the products offered at our store.</div>\r\n			</div>\r\n		</div>\r\n		<div class="col-xs-12 col-sm-3">\r\n			<div class="team">\r\n				<a title="EDNA BARTON" href="#"><img alt="EDNA BARTON" src="{{media url="wysiwyg/fasony/about/about-04.jpg"}}"></a>\r\n				<h4><a title="EDNA BARTON" href="#">EDNA BARTON</a></h4>\r\n				<div class="excerpt">Quality control manager. Her mission is to check the products we ship and settle quality issues if any.</div>\r\n			</div>\r\n		</div>\r\n	</div>\r\n</div>', '2016-04-23 07:15:49', '2016-04-23 09:16:48', 1),
(12, 'Fasony Banner Sidebar', 'fasony-banner-sidebar', '<div class="block sidebar-image">\r\n	<img alt="" src="{{media url="wysiwyg/fasony/detail/banner1.jpg"}}" class="img-responsive">\r\n</div> \r\n', '2016-04-25 10:14:04', '2016-04-25 10:19:46', 1),
(13, 'Fasony custom block', 'fasony-custom-block', '<div class="block custom-block">\r\n	<div>\r\n		<em class="fa fa-truck"></em>\r\n		<h3>FREE SHIPPING</h3>\r\n		<p>Free shipping on all orders over $99.</p>\r\n	</div>\r\n	<div>\r\n		<em class="fa fa-money"></em>\r\n		<h3>MONEY BACK</h3>\r\n		<p>100% money back guarantee.</p>\r\n	</div>\r\n	<div>\r\n		<em class="fa fa-life-ring"></em>\r\n		<h3>ONLINE SUPPORT 24/7</h3>\r\n		<p>Unlimited time support.</p>\r\n	</div>\r\n</div>', '2016-04-25 10:23:33', '2016-04-25 10:23:33', 1),
(14, 'Fasony Sidebar Products2', 'fasony-sidebar-products2', '<p>{{widget type="Magento\\Catalog\\Block\\Product\\Widget\\NewWidget" display_type="all_products" products_count="3" template="product/widget/new/content/new_list.phtml"}}</p>', '2016-04-25 10:26:12', '2016-04-25 10:26:12', 1);

-- --------------------------------------------------------

--
-- Table structure for table `cms_block_store`
--

CREATE TABLE `cms_block_store` (
  `block_id` smallint(6) NOT NULL COMMENT 'Block ID',
  `store_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Store ID'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='CMS Block To Store Linkage Table';

--
-- Dumping data for table `cms_block_store`
--

INSERT INTO `cms_block_store` (`block_id`, `store_id`) VALUES
(1, 0),
(2, 0),
(3, 0),
(4, 0),
(5, 0),
(6, 0),
(7, 0),
(8, 0),
(9, 0),
(10, 0),
(11, 0),
(12, 0),
(13, 0),
(14, 0);

-- --------------------------------------------------------

--
-- Table structure for table `cms_page`
--

CREATE TABLE `cms_page` (
  `page_id` smallint(6) NOT NULL COMMENT 'Page ID',
  `title` varchar(255) DEFAULT NULL COMMENT 'Page Title',
  `page_layout` varchar(255) DEFAULT NULL COMMENT 'Page Layout',
  `meta_keywords` text COMMENT 'Page Meta Keywords',
  `meta_description` text COMMENT 'Page Meta Description',
  `identifier` varchar(100) DEFAULT NULL COMMENT 'Page String Identifier',
  `content_heading` varchar(255) DEFAULT NULL COMMENT 'Page Content Heading',
  `content` mediumtext COMMENT 'Page Content',
  `creation_time` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT 'Page Creation Time',
  `update_time` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP COMMENT 'Page Modification Time',
  `is_active` smallint(6) NOT NULL DEFAULT '1' COMMENT 'Is Page Active',
  `sort_order` smallint(6) NOT NULL DEFAULT '0' COMMENT 'Page Sort Order',
  `layout_update_xml` text COMMENT 'Page Layout Update Content',
  `custom_theme` varchar(100) DEFAULT NULL COMMENT 'Page Custom Theme',
  `custom_root_template` varchar(255) DEFAULT NULL COMMENT 'Page Custom Template',
  `custom_layout_update_xml` text COMMENT 'Page Custom Layout Update Content',
  `custom_theme_from` date DEFAULT NULL COMMENT 'Page Custom Theme Active From Date',
  `custom_theme_to` date DEFAULT NULL COMMENT 'Page Custom Theme Active To Date'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='CMS Page Table';

--
-- Dumping data for table `cms_page`
--

INSERT INTO `cms_page` (`page_id`, `title`, `page_layout`, `meta_keywords`, `meta_description`, `identifier`, `content_heading`, `content`, `creation_time`, `update_time`, `is_active`, `sort_order`, `layout_update_xml`, `custom_theme`, `custom_root_template`, `custom_layout_update_xml`, `custom_theme_from`, `custom_theme_to`) VALUES
(1, '404 Not Found', '2columns-right', 'Page keywords', 'Page description', 'no-route', 'Whoops, our bad...', '<dl>\r\n<dt>The page you requested was not found, and we have a fine guess why.</dt>\r\n<dd>\r\n<ul class="disc">\r\n<li>If you typed the URL directly, please make sure the spelling is correct.</li>\r\n<li>If you clicked on a link to get here, the link is outdated.</li>\r\n</ul></dd>\r\n</dl>\r\n<dl>\r\n<dt>What can you do?</dt>\r\n<dd>Have no fear, help is near! There are many ways you can get back on track with Magento Store.</dd>\r\n<dd>\r\n<ul class="disc">\r\n<li><a href="#" onclick="history.go(-1); return false;">Go back</a> to the previous page.</li>\r\n<li>Use the search bar at the top of the page to search for your products.</li>\r\n<li>Follow these links to get you back on track!<br /><a href="{{store url=""}}">Store Home</a> <span class="separator">|</span> <a href="{{store url="customer/account"}}">My Account</a></li></ul></dd></dl>\r\n', '2016-04-12 14:15:44', '2016-04-12 14:15:44', 1, 0, NULL, NULL, NULL, NULL, NULL, NULL),
(2, 'Home page', '1column', NULL, NULL, 'home', 'Home Page', '<div class="hidden">CMS homepage content goes here.</div>', '2016-04-12 14:15:45', '2016-04-15 09:24:41', 1, 0, '<referenceContainer name="ves-slideshow">\r\n	<block class="Magento\\Cms\\Block\\Block" name="fasony-slideshow-banner">\r\n		<arguments>\r\n			<argument name="block_id" xsi:type="string">fasony-slideshow-banner</argument>\r\n		</arguments>\r\n	</block>\r\n</referenceContainer>\r\n\r\n<referenceContainer name="ves-showcase">\r\n	<block class="Magento\\Cms\\Block\\Block" name="fasony-showcase-category">\r\n		<arguments>\r\n			<argument name="block_id" xsi:type="string">fasony-showcase-category</argument>\r\n		</arguments>\r\n	</block>\r\n</referenceContainer>\r\n\r\n<referenceContainer name="ves-masstop">\r\n	<block class="Magento\\Cms\\Block\\Block" name="fasony-newproducts">\r\n		<arguments>\r\n			<argument name="block_id" xsi:type="string">fasony-newproducts</argument>\r\n		</arguments>\r\n	</block>\r\n</referenceContainer>\r\n\r\n<referenceContainer name="ves-massbottom">\r\n	<block class="Magento\\Cms\\Block\\Block" name="fasony-ourservice">\r\n		<arguments>\r\n			<argument name="block_id" xsi:type="string">fasony-ourservice</argument>\r\n		</arguments>\r\n	</block>\r\n</referenceContainer>\r\n\r\n<referenceContainer name="ves-massbottom1">\r\n	<block class="Magento\\Cms\\Block\\Block" name="fasony-testominial">\r\n		<arguments>\r\n			<argument name="block_id" xsi:type="string">fasony-testominial</argument>\r\n		</arguments>\r\n	</block>\r\n</referenceContainer>\r\n\r\n<referenceContainer name="ves-massbottom2">\r\n	<block class="Magento\\Cms\\Block\\Block" name="fasony-ourbrands">\r\n		<arguments>\r\n			<argument name="block_id" xsi:type="string">fasony-ourbrands</argument>\r\n		</arguments>\r\n	</block>\r\n</referenceContainer>', NULL, NULL, NULL, NULL, NULL),
(3, 'Enable Cookies', '1column', NULL, NULL, 'enable-cookies', 'What are Cookies?', '<div class="enable-cookies cms-content">\r\n<p>"Cookies" are little pieces of data we send when you visit our store. Cookies help us get to know you better and personalize your experience. Plus they help protect you and other shoppers from fraud.</p>\r\n<p style="margin-bottom: 20px;">Set your browser to accept cookies so you can buy items, save items, and receive customized recommendations. Here’s how:</p>\r\n<ul>\r\n<li><a href="https://support.google.com/accounts/answer/61416?hl=en" target="_blank">Google Chrome</a></li>\r\n<li><a href="http://windows.microsoft.com/en-us/internet-explorer/delete-manage-cookies" target="_blank">Internet Explorer</a></li>\r\n<li><a href="http://support.apple.com/kb/PH19214" target="_blank">Safari</a></li>\r\n<li><a href="https://support.mozilla.org/en-US/kb/enable-and-disable-cookies-website-preferences" target="_blank">Mozilla/Firefox</a></li>\r\n</ul>\r\n</div>', '2016-04-12 14:15:45', '2016-04-12 14:15:45', 1, 0, NULL, NULL, NULL, NULL, NULL, NULL),
(4, 'Privacy and Cookie Policy', '1column', NULL, NULL, 'privacy-policy-cookie-restriction-mode', 'Privacy and Cookie Policy', '<div class="privacy-policy cms-content">\n    <div class="message info">\n        <span>\n            Please replace this text with you Privacy Policy.\n            Please add any additional cookies your website uses below (e.g. Google Analytics).\n        </span>\n    </div>\n    <p>\n        This privacy policy sets out how this website (hereafter "the Store") uses and protects any information that\n        you give the Store while using this website. The Store is committed to ensuring that your privacy is protected.\n        Should we ask you to provide certain information by which you can be identified when using this website, then\n        you can be assured that it will only be used in accordance with this privacy statement. The Store may change\n        this policy from time to time by updating this page. You should check this page from time to time to ensure\n        that you are happy with any changes.\n    </p>\n    <h2>What we collect</h2>\n    <p>We may collect the following information:</p>\n    <ul>\n        <li>name</li>\n        <li>contact information including email address</li>\n        <li>demographic information such as postcode, preferences and interests</li>\n        <li>other information relevant to customer surveys and/or offers</li>\n    </ul>\n    <p>\n        For the exhaustive list of cookies we collect see the <a href="#list">List of cookies we collect</a> section.\n    </p>\n    <h2>What we do with the information we gather</h2>\n    <p>\n        We require this information to understand your needs and provide you with a better service,\n        and in particular for the following reasons:\n    </p>\n    <ul>\n        <li>Internal record keeping.</li>\n        <li>We may use the information to improve our products and services.</li>\n        <li>\n            We may periodically send promotional emails about new products, special offers or other information which we\n            think you may find interesting using the email address which you have provided.\n        </li>\n        <li>\n            From time to time, we may also use your information to contact you for market research purposes.\n            We may contact you by email, phone, fax or mail. We may use the information to customise the website\n            according to your interests.\n        </li>\n    </ul>\n    <h2>Security</h2>\n    <p>\n        We are committed to ensuring that your information is secure. In order to prevent unauthorised access or\n        disclosure, we have put in place suitable physical, electronic and managerial procedures to safeguard and\n        secure the information we collect online.\n    </p>\n    <h2>How we use cookies</h2>\n    <p>\n        A cookie is a small file which asks permission to be placed on your computer''s hard drive.\n        Once you agree, the file is added and the cookie helps analyse web traffic or lets you know when you visit\n        a particular site. Cookies allow web applications to respond to you as an individual. The web application\n        can tailor its operations to your needs, likes and dislikes by gathering and remembering information about\n        your preferences.\n    </p>\n    <p>\n        We use traffic log cookies to identify which pages are being used. This helps us analyse data about web page\n        traffic and improve our website in order to tailor it to customer needs. We only use this information for\n        statistical analysis purposes and then the data is removed from the system.\n    </p>\n    <p>\n        Overall, cookies help us provide you with a better website, by enabling us to monitor which pages you find\n        useful and which you do not. A cookie in no way gives us access to your computer or any information about you,\n        other than the data you choose to share with us. You can choose to accept or decline cookies.\n        Most web browsers automatically accept cookies, but you can usually modify your browser setting\n        to decline cookies if you prefer. This may prevent you from taking full advantage of the website.\n    </p>\n    <h2>Links to other websites</h2>\n    <p>\n        Our website may contain links to other websites of interest. However, once you have used these links\n        to leave our site, you should note that we do not have any control over that other website.\n        Therefore, we cannot be responsible for the protection and privacy of any information which you provide whilst\n        visiting such sites and such sites are not governed by this privacy statement.\n        You should exercise caution and look at the privacy statement applicable to the website in question.\n    </p>\n    <h2>Controlling your personal information</h2>\n    <p>You may choose to restrict the collection or use of your personal information in the following ways:</p>\n    <ul>\n        <li>\n            whenever you are asked to fill in a form on the website, look for the box that you can click to indicate\n            that you do not want the information to be used by anybody for direct marketing purposes\n        </li>\n        <li>\n            if you have previously agreed to us using your personal information for direct marketing purposes,\n            you may change your mind at any time by letting us know using our Contact Us information\n        </li>\n    </ul>\n    <p>\n        We will not sell, distribute or lease your personal information to third parties unless we have your permission\n        or are required by law to do so. We may use your personal information to send you promotional information\n        about third parties which we think you may find interesting if you tell us that you wish this to happen.\n    </p>\n    <p>\n        You may request details of personal information which we hold about you under the Data Protection Act 1998.\n        A small fee will be payable. If you would like a copy of the information held on you please email us this\n        request using our Contact Us information.\n    </p>\n    <p>\n        If you believe that any information we are holding on you is incorrect or incomplete,\n        please write to or email us as soon as possible, at the above address.\n        We will promptly correct any information found to be incorrect.\n    </p>\n    <h2><a name="list"></a>List of cookies we collect</h2>\n    <p>The table below lists the cookies we collect and what information they store.</p>\n    <table class="data-table">\n        <thead>\n            <tr>\n                <th>COOKIE name</th>\n                <th>COOKIE Description</th>\n            </tr>\n        </thead>\n        <tbody>\n            <tr>\n                <th>CART</th>\n                <td>The association with your shopping cart.</td>\n            </tr>\n            <tr>\n                <th>CATEGORY_INFO</th>\n                <td>Stores the category info on the page, that allows to display pages more quickly.</td>\n            </tr>\n            <tr>\n                <th>COMPARE</th>\n                <td>The items that you have in the Compare Products list.</td>\n            </tr>\n            <tr>\n                <th>CUSTOMER</th>\n                <td>An encrypted version of your customer id with the store.</td>\n            </tr>\n            <tr>\n                <th>CUSTOMER_AUTH</th>\n                <td>An indicator if you are currently logged into the store.</td>\n            </tr>\n            <tr>\n                <th>CUSTOMER_INFO</th>\n                <td>An encrypted version of the customer group you belong to.</td>\n            </tr>\n            <tr>\n                <th>CUSTOMER_SEGMENT_IDS</th>\n                <td>Stores the Customer Segment ID</td>\n            </tr>\n            <tr>\n                <th>EXTERNAL_NO_CACHE</th>\n                <td>A flag, which indicates whether caching is disabled or not.</td>\n            </tr>\n            <tr>\n                <th>FORM_KEY</th>\n                <td>Stores form key used by page cache functionality.</td>\n            </tr>\n            <tr>\n                <th>FRONTEND</th>\n                <td>Your session ID on the server.</td>\n            </tr>\n            <tr>\n                <th>GUEST-VIEW</th>\n                <td>Allows guests to edit their orders.</td>\n            </tr>\n            <tr>\n                <th>LAST_CATEGORY</th>\n                <td>The last category you visited.</td>\n            </tr>\n            <tr>\n                <th>LAST_PRODUCT</th>\n                <td>The most recent product you have viewed.</td>\n            </tr>\n            <tr>\n                <th>NEWMESSAGE</th>\n                <td>Indicates whether a new message has been received.</td>\n            </tr>\n            <tr>\n                <th>NO_CACHE</th>\n                <td>Indicates whether it is allowed to use cache.</td>\n            </tr>\n            <tr>\n                <th>PERSISTENT_SHOPPING_CART</th>\n                <td>A link to information about your cart and viewing history if you have asked the site.</td>\n            </tr>\n            <tr>\n                <th>RECENTLYCOMPARED</th>\n                <td>The items that you have recently compared.</td>\n            </tr>\n            <tr>\n                <th>STF</th>\n                <td>Information on products you have emailed to friends.</td>\n            </tr>\n            <tr>\n                <th>STORE</th>\n                <td>The store view or language you have selected.</td>\n            </tr>\n            <tr>\n                <th>USER_ALLOWED_SAVE_COOKIE</th>\n                <td>Indicates whether a customer allowed to use cookies.</td>\n            </tr>\n            <tr>\n                <th>VIEWED_PRODUCT_IDS</th>\n                <td>The products that you have recently viewed.</td>\n            </tr>\n            <tr>\n                <th>WISHLIST</th>\n                <td>An encrypted list of products added to your Wish List.</td>\n            </tr>\n            <tr>\n                <th>WISHLIST_CNT</th>\n                <td>The number of items in your Wish List.</td>\n            </tr>\n        </tbody>\n    </table>\n</div>', '2016-04-12 14:15:45', '2016-04-12 14:15:45', 1, 0, NULL, NULL, NULL, NULL, NULL, NULL),
(5, 'A New Era of Commerce Innovation', '1column', NULL, NULL, 'blog-detail', NULL, '<div class="post-content-wrap">\r\n<div class="post-image"><img src="{{media url="wysiwyg/fasony/blogs/blog-detail.jpg"}}" alt="A New Era of Commerce Innovation" /></div>\r\n<div class="post-meta">\r\n<div class="post-title">\r\n<h3>A New Era of Commerce Innovation</h3>\r\n</div>\r\n<div class="post-author">Posted by: <a title="" href="{{store url=''blog-detail.html''}}">venusadmin venusadmin</a></div>\r\n<div class="post-date"><span>Created on Feb 5, 2016</span> <span>Updated on Feb 5, 2016</span></div>\r\n<div class="post-comment">0 comments</div>\r\n<div class="post-categories">Pubslished In: <a title="Customer Stories" href="{{store url=''blog-detail.html''}}">Customer Stories</a>, <a title="Technical" href="{{store url=''blog-detail.html''}}">Technical</a>, <a title="Events" href="{{store url=''blog-detail.html''}}">Events</a>, <a title="Magento News" href="{{store url=''blog-detail.html''}}">Magento News</a></div>\r\n<div class="post-hits"><span>Read</span> <strong>27</strong> Times</div>\r\n</div>\r\n<div class="post-content">\r\n<div class="field-item even">\r\n<p>Today we announced the general availability of our next generation open source digital commerce platform, Magento 2.0.&nbsp; The new platform empowers brands, retailers, and businesses across B2C and B2B industries to quickly and cost-effectively deliver engaging omnichannel shopping experiences. Magento 2.0 also offers enhanced performance and scalability, &nbsp;new features to boost conversion rates, and business agility and productivity improvements. The new platform also builds on our open source heritage and offers unmatched flexibility and innovation opportunities to our global ecosystem of partners and developers.</p>\r\n<p>Two new products based on this powerful platform are available for download today: Magento Enterprise Edition 2.0 and Magento Community Edition 2.0.</p>\r\n<p><strong>Open, Flexible Architecture</strong></p>\r\n<p>Underpinning these new releases is a next-generation architecture that offers unmatched flexibility to bring your commerce vision to life. It features a modular code base that enables easier customization, faster time-to-market, and greater deployment flexibility to public or private cloud environments. More extensive and efficient APIs allow you to connect and operate at scale with any third party solution, and theming capabilities make building site variations for new product lines or geographies easier than ever. A wide range of turnkey extensions also enable fast and affordable enhancements to your store.</p>\r\n<p><strong>Engaging Shopping Experiences</strong></p>\r\n<p>Creating engaging, seamless and personalized customer experiences across any device is central to the Magento 2.0 platform. New responsive design reference themes give you a fast way to create sites that supports anytime, anywhere sales. And you can share your products in a more immersive way through integrated video. An all-new checkout is easier to customize and further improves conversion rates by minimizing steps and required information. You can also offer convenient, one-click account creation to save customer profiles for future purchases.&nbsp;</p>\r\n<p><strong>Enhanced Business Agility and Productivity</strong></p>\r\n<p>Magento Commerce is also revolutionizing the merchant experience, enabling you to operate more efficiently and handle rapid growth, without scaling up your team. The new Admin panel design offers a streamlined, consumer-like interface that saves time when managing day-to-day tasks and is intuitive for new team members to learn. It is also touch-friendly so you can make updates or track sales while on-the-go.</p>\r\n<p>Improved business tools empower you to continuously optimize your operations to drive growth. You can now effortlessly customize and save views in the Admin panel to enable quick access to information critical to your business. Setting up new products is also faster, with a step-by-step product creation tool and product import capabilities that are 4x faster than before.</p>\r\n<p><strong>Enterprise-grade Scalability and Performance</strong></p>\r\n<p>The Magento platform has been supercharged to offer over 50% faster page load times across many catalog and checkout pages to help you delight your customers and improve conversion rates. It&nbsp;<span>pre-integrates Varnish to cache page content for faster performance and optimizes code and images for fast loading. Your team will be delighted too, with improved Admin performance and support for more concurrent updates. Magento Enterprise Edition 2.0 also delivers enterprise-grade scalability and high availability with standalone master databases for key subsystems along with multiple slave databases.</span></p>\r\n<p><strong>Secure Payments</strong></p>\r\n<p>Additionally, the Magento platform comes with tight out-of-the-box integrations with PayPal, Braintree, and Authorize.net payment gateways. Magento Enterprise Edition 2.0 also integrates with WorldPay and CyberSource. &nbsp;All versions provide improved security and the ability to pursue the easiest level of PCI compliance, depending on the selected payment method.</p>\r\n<p><strong>Easier Maintenance and Upgrades</strong></p>\r\n<p>And finally, this modern, modular architecture reduces the complexity and cost of maintaining your site and it futureproofs your investment by simplifying upgrades. This means you can easily incorporate innovative functionality as it is released by Magento Commerce on a quarterly basis to drive higher sales and greater efficiency.</p>\r\n<p><strong>Start Exploring Today</strong></p>\r\n<p>There are many ways to learn more about the powerful and innovative Magento Commerce platform:</p>\r\n<ul>\r\n<li>\r\n<p>To access product information, videos, and white papers visit the <a href="{{store url=''blog-detail.html''}}" target="_blank">Magento Enterprise Edition page</a>.</p>\r\n</li>\r\n<li>\r\n<p>To learn more about merchants already deployed on Magento Enterprise Edition 2.0, check out our <a href="{{store url=''blog-detail.html''}}" target="_blank">early adopter blog post</a>.</p>\r\n</li>\r\n<li>\r\n<p>To find a Magento 2.0 Trained Solution Partner visit the <a href="{{store url=''blog-detail.html''}}" target="_blank">Partner Directory</a>&nbsp;or the <a href="{{store url=''blog-detail.html''}}" target="_blank">blog post</a></p>\r\n</li>\r\n<li>\r\n<p>To see all the extensions available for Magento 2.0, visit our dedicated <a href="{{store url=''blog-detail.html''}}" target="_blank">extension page</a>.</p>\r\n</li>\r\n</ul>\r\n<p>You can also start using the new software today. Existing Enterprise Edition customers can access it via <a href="{{store url=''blog-detail.html''}}" target="_blank">MyAccount</a> &nbsp;and Community Edition users can download it from the Community Edition <a href="{{store url=''blog-detail.html''}}" target="_blank">download page</a>.</p>\r\n<p><span style="line-height: 1.6em;">Welcome to next-generation commerce!</span></p>\r\n</div>\r\n</div>\r\n<div class="post-meta">\r\n<div class="post-tag"><span>Tags:</span> <a href="{{store url=''blog-detail.html''}}">Business News</a>, <a href="{{store url=''blog-detail.html''}}"> Enterprise Edition</a>, <a href="{{store url=''blog-detail.html''}}"> Magento 2</a>, <a href="{{store url=''blog-detail.html''}}"> Products</a></div>\r\n</div>\r\n</div>', '2016-04-23 03:35:58', '2016-04-23 03:39:54', 1, 0, NULL, NULL, NULL, NULL, NULL, NULL);

-- --------------------------------------------------------

--
-- Table structure for table `cms_page_store`
--

CREATE TABLE `cms_page_store` (
  `page_id` smallint(6) NOT NULL COMMENT 'Page ID',
  `store_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Store ID'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='CMS Page To Store Linkage Table';

--
-- Dumping data for table `cms_page_store`
--

INSERT INTO `cms_page_store` (`page_id`, `store_id`) VALUES
(1, 0),
(2, 0),
(3, 0),
(4, 0),
(5, 0);

-- --------------------------------------------------------

--
-- Table structure for table `core_config_data`
--

CREATE TABLE `core_config_data` (
  `config_id` int(10) UNSIGNED NOT NULL COMMENT 'Config Id',
  `scope` varchar(8) NOT NULL DEFAULT 'default' COMMENT 'Config Scope',
  `scope_id` int(11) NOT NULL DEFAULT '0' COMMENT 'Config Scope Id',
  `path` varchar(255) NOT NULL DEFAULT 'general' COMMENT 'Config Path',
  `value` text COMMENT 'Config Value'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Config Data';

--
-- Dumping data for table `core_config_data`
--

INSERT INTO `core_config_data` (`config_id`, `scope`, `scope_id`, `path`, `value`) VALUES
(1, 'default', 0, 'web/seo/use_rewrites', '1'),
(2, 'default', 0, 'web/unsecure/base_url', 'http://localhost/ves_fasony/'),
(3, 'default', 0, 'web/secure/base_url', 'https://localhost/ves_fasony/'),
(4, 'default', 0, 'general/locale/code', 'en_US'),
(5, 'default', 0, 'web/secure/use_in_frontend', NULL),
(6, 'default', 0, 'web/secure/use_in_adminhtml', NULL),
(7, 'default', 0, 'general/locale/timezone', 'UTC'),
(8, 'default', 0, 'currency/options/base', 'USD'),
(9, 'default', 0, 'currency/options/default', 'USD'),
(10, 'default', 0, 'currency/options/allow', 'EUR,USD'),
(11, 'default', 0, 'general/region/display_all', '1'),
(12, 'default', 0, 'general/region/state_required', 'AT,BR,CA,CH,DE,EE,ES,FI,FR,LT,LV,RO,US'),
(13, 'default', 0, 'catalog/category/root_id', NULL),
(14, 'default', 0, 'design/theme/theme_id', '4'),
(15, 'default', 0, 'design/theme/ua_regexp', 'a:0:{}'),
(16, 'default', 0, 'design/head/default_title', 'Magento Commerce'),
(17, 'default', 0, 'design/head/title_prefix', NULL),
(18, 'default', 0, 'design/head/title_suffix', NULL),
(19, 'default', 0, 'design/head/default_description', 'Default Description'),
(20, 'default', 0, 'design/head/default_keywords', 'Magento, Varien, E-commerce'),
(21, 'default', 0, 'design/head/includes', NULL),
(22, 'default', 0, 'design/head/demonotice', '0'),
(23, 'default', 0, 'design/head/shortcut_icon', NULL),
(24, 'default', 0, 'design/search_engine_robots/default_robots', 'INDEX,FOLLOW'),
(25, 'default', 0, 'design/search_engine_robots/custom_instructions', NULL),
(26, 'default', 0, 'design/header/logo_width', NULL),
(27, 'default', 0, 'design/header/logo_height', NULL),
(28, 'default', 0, 'design/header/logo_alt', 'Magento Commerce'),
(29, 'default', 0, 'design/header/welcome', 'Default welcome msg!'),
(30, 'default', 0, 'design/header/logo_src', 'default/logo.png'),
(31, 'default', 0, 'design/footer/copyright', 'Copyright © 2016 Magento. All rights reserved.'),
(32, 'default', 0, 'design/footer/absolute_footer', NULL),
(33, 'default', 0, 'design/watermark/image_size', NULL),
(34, 'default', 0, 'design/watermark/image_imageOpacity', NULL),
(35, 'default', 0, 'design/watermark/image_position', 'stretch'),
(36, 'default', 0, 'design/watermark/small_image_size', NULL),
(37, 'default', 0, 'design/watermark/small_image_imageOpacity', NULL),
(38, 'default', 0, 'design/watermark/small_image_position', 'stretch'),
(39, 'default', 0, 'design/watermark/swatch_image_size', NULL),
(40, 'default', 0, 'design/watermark/swatch_image_imageOpacity', NULL),
(41, 'default', 0, 'design/watermark/swatch_image_position', 'stretch'),
(42, 'default', 0, 'design/watermark/thumbnail_size', NULL),
(43, 'default', 0, 'design/watermark/thumbnail_imageOpacity', NULL),
(44, 'default', 0, 'design/watermark/thumbnail_position', 'stretch'),
(45, 'default', 0, 'design/watermark/image_image', NULL),
(46, 'default', 0, 'design/watermark/small_image_image', NULL),
(47, 'default', 0, 'design/watermark/swatch_image_image', NULL),
(48, 'default', 0, 'design/watermark/thumbnail_image', NULL),
(49, 'default', 0, 'design/pagination/pagination_frame', '5'),
(50, 'default', 0, 'design/pagination/pagination_frame_skip', NULL),
(51, 'default', 0, 'design/pagination/anchor_text_for_previous', NULL),
(52, 'default', 0, 'design/pagination/anchor_text_for_next', NULL),
(53, 'default', 0, 'design/email/logo_alt', NULL),
(54, 'default', 0, 'design/email/logo_width', NULL),
(55, 'default', 0, 'design/email/logo_height', NULL),
(56, 'default', 0, 'design/email/header_template', 'design_email_header_template'),
(57, 'default', 0, 'design/email/footer_template', 'design_email_footer_template'),
(58, 'default', 0, 'design/email/logo', NULL),
(59, 'default', 0, 'currency/webservicex/timeout', '100'),
(60, 'default', 0, 'currency/import/enabled', '0'),
(61, 'default', 0, 'currency/import/service', 'webservicex'),
(62, 'default', 0, 'crontab/default/jobs/currency_rates_update/schedule/cron_expr', '0 0 * * *'),
(63, 'default', 0, 'currency/import/time', '00,00,00'),
(64, 'default', 0, 'currency/import/frequency', 'D'),
(65, 'default', 0, 'currency/import/error_email', NULL),
(66, 'default', 0, 'currency/import/error_email_identity', 'general'),
(67, 'default', 0, 'currency/import/error_email_template', 'currency_import_error_email_template');

-- --------------------------------------------------------

--
-- Table structure for table `cron_schedule`
--

CREATE TABLE `cron_schedule` (
  `schedule_id` int(10) UNSIGNED NOT NULL COMMENT 'Schedule Id',
  `job_code` varchar(255) NOT NULL DEFAULT '0' COMMENT 'Job Code',
  `status` varchar(7) NOT NULL DEFAULT 'pending' COMMENT 'Status',
  `messages` text COMMENT 'Messages',
  `created_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT 'Created At',
  `scheduled_at` timestamp NULL DEFAULT NULL COMMENT 'Scheduled At',
  `executed_at` timestamp NULL DEFAULT NULL COMMENT 'Executed At',
  `finished_at` timestamp NULL DEFAULT NULL COMMENT 'Finished At'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Cron Schedule';

-- --------------------------------------------------------

--
-- Table structure for table `customer_address_entity`
--

CREATE TABLE `customer_address_entity` (
  `entity_id` int(10) UNSIGNED NOT NULL COMMENT 'Entity Id',
  `increment_id` varchar(50) DEFAULT NULL COMMENT 'Increment Id',
  `parent_id` int(10) UNSIGNED DEFAULT NULL COMMENT 'Parent Id',
  `created_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT 'Created At',
  `updated_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP COMMENT 'Updated At',
  `is_active` smallint(5) UNSIGNED NOT NULL DEFAULT '1' COMMENT 'Is Active',
  `city` varchar(255) NOT NULL COMMENT 'City',
  `company` varchar(255) DEFAULT NULL COMMENT 'Company',
  `country_id` varchar(255) NOT NULL COMMENT 'Country',
  `fax` varchar(255) DEFAULT NULL COMMENT 'Fax',
  `firstname` varchar(255) NOT NULL COMMENT 'First Name',
  `lastname` varchar(255) NOT NULL COMMENT 'Last Name',
  `middlename` varchar(255) DEFAULT NULL COMMENT 'Middle Name',
  `postcode` varchar(255) DEFAULT NULL COMMENT 'Zip/Postal Code',
  `prefix` varchar(40) DEFAULT NULL COMMENT 'Prefix',
  `region` varchar(255) DEFAULT NULL COMMENT 'State/Province',
  `region_id` int(10) UNSIGNED DEFAULT NULL COMMENT 'State/Province',
  `street` text NOT NULL COMMENT 'Street Address',
  `suffix` varchar(40) DEFAULT NULL COMMENT 'Suffix',
  `telephone` varchar(255) NOT NULL COMMENT 'Phone Number',
  `vat_id` varchar(255) DEFAULT NULL COMMENT 'VAT number',
  `vat_is_valid` int(10) UNSIGNED DEFAULT NULL COMMENT 'VAT number validity',
  `vat_request_date` varchar(255) DEFAULT NULL COMMENT 'VAT number validation request date',
  `vat_request_id` varchar(255) DEFAULT NULL COMMENT 'VAT number validation request ID',
  `vat_request_success` int(10) UNSIGNED DEFAULT NULL COMMENT 'VAT number validation request success'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Customer Address Entity';

--
-- Dumping data for table `customer_address_entity`
--

INSERT INTO `customer_address_entity` (`entity_id`, `increment_id`, `parent_id`, `created_at`, `updated_at`, `is_active`, `city`, `company`, `country_id`, `fax`, `firstname`, `lastname`, `middlename`, `postcode`, `prefix`, `region`, `region_id`, `street`, `suffix`, `telephone`, `vat_id`, `vat_is_valid`, `vat_request_date`, `vat_request_id`, `vat_request_success`) VALUES
(1, NULL, 1, '2016-04-27 08:11:00', '2016-04-27 08:11:00', 1, 'Ha Noi', 'Brainos', 'US', NULL, 'Le', 'Lieu', NULL, '12345', NULL, 'Alabama', 1, 'MD', NULL, '123456789', NULL, NULL, NULL, NULL, NULL),
(2, NULL, 2, '2016-04-28 03:06:20', '2016-04-28 03:06:20', 1, 'Ha Noi', 'TNT', 'US', NULL, 'Le', 'Lieu', NULL, '12345', NULL, 'Alabama', 1, 'MD', NULL, '123456789', NULL, NULL, NULL, NULL, NULL);

-- --------------------------------------------------------

--
-- Table structure for table `customer_address_entity_datetime`
--

CREATE TABLE `customer_address_entity_datetime` (
  `value_id` int(11) NOT NULL COMMENT 'Value Id',
  `attribute_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Attribute Id',
  `entity_id` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Entity Id',
  `value` datetime DEFAULT NULL COMMENT 'Value'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Customer Address Entity Datetime';

-- --------------------------------------------------------

--
-- Table structure for table `customer_address_entity_decimal`
--

CREATE TABLE `customer_address_entity_decimal` (
  `value_id` int(11) NOT NULL COMMENT 'Value Id',
  `attribute_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Attribute Id',
  `entity_id` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Entity Id',
  `value` decimal(12,4) NOT NULL DEFAULT '0.0000' COMMENT 'Value'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Customer Address Entity Decimal';

-- --------------------------------------------------------

--
-- Table structure for table `customer_address_entity_int`
--

CREATE TABLE `customer_address_entity_int` (
  `value_id` int(11) NOT NULL COMMENT 'Value Id',
  `attribute_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Attribute Id',
  `entity_id` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Entity Id',
  `value` int(11) NOT NULL DEFAULT '0' COMMENT 'Value'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Customer Address Entity Int';

-- --------------------------------------------------------

--
-- Table structure for table `customer_address_entity_text`
--

CREATE TABLE `customer_address_entity_text` (
  `value_id` int(11) NOT NULL COMMENT 'Value Id',
  `attribute_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Attribute Id',
  `entity_id` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Entity Id',
  `value` text NOT NULL COMMENT 'Value'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Customer Address Entity Text';

-- --------------------------------------------------------

--
-- Table structure for table `customer_address_entity_varchar`
--

CREATE TABLE `customer_address_entity_varchar` (
  `value_id` int(11) NOT NULL COMMENT 'Value Id',
  `attribute_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Attribute Id',
  `entity_id` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Entity Id',
  `value` varchar(255) DEFAULT NULL COMMENT 'Value'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Customer Address Entity Varchar';

-- --------------------------------------------------------

--
-- Table structure for table `customer_eav_attribute`
--

CREATE TABLE `customer_eav_attribute` (
  `attribute_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Attribute Id',
  `is_visible` smallint(5) UNSIGNED NOT NULL DEFAULT '1' COMMENT 'Is Visible',
  `input_filter` varchar(255) DEFAULT NULL COMMENT 'Input Filter',
  `multiline_count` smallint(5) UNSIGNED NOT NULL DEFAULT '1' COMMENT 'Multiline Count',
  `validate_rules` text COMMENT 'Validate Rules',
  `is_system` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Is System',
  `sort_order` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Sort Order',
  `data_model` varchar(255) DEFAULT NULL COMMENT 'Data Model',
  `is_used_in_grid` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Is Used in Grid',
  `is_visible_in_grid` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Is Visible in Grid',
  `is_filterable_in_grid` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Is Filterable in Grid',
  `is_searchable_in_grid` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Is Searchable in Grid'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Customer Eav Attribute';

--
-- Dumping data for table `customer_eav_attribute`
--

INSERT INTO `customer_eav_attribute` (`attribute_id`, `is_visible`, `input_filter`, `multiline_count`, `validate_rules`, `is_system`, `sort_order`, `data_model`, `is_used_in_grid`, `is_visible_in_grid`, `is_filterable_in_grid`, `is_searchable_in_grid`) VALUES
(1, 1, NULL, 0, NULL, 1, 10, NULL, 1, 1, 1, 0),
(2, 0, NULL, 0, NULL, 1, 0, NULL, 0, 0, 0, 0),
(3, 1, NULL, 0, NULL, 1, 20, NULL, 1, 1, 0, 1),
(4, 0, NULL, 0, NULL, 0, 30, NULL, 0, 0, 0, 0),
(5, 1, NULL, 0, 'a:2:{s:15:"max_text_length";i:255;s:15:"min_text_length";i:1;}', 1, 40, NULL, 0, 0, 0, 0),
(6, 0, NULL, 0, NULL, 0, 50, NULL, 0, 0, 0, 0),
(7, 1, NULL, 0, 'a:2:{s:15:"max_text_length";i:255;s:15:"min_text_length";i:1;}', 1, 60, NULL, 0, 0, 0, 0),
(8, 0, NULL, 0, NULL, 0, 70, NULL, 0, 0, 0, 0),
(9, 1, NULL, 0, 'a:1:{s:16:"input_validation";s:5:"email";}', 1, 80, NULL, 1, 1, 1, 1),
(10, 1, NULL, 0, NULL, 1, 25, NULL, 1, 1, 1, 0),
(11, 0, 'date', 0, 'a:1:{s:16:"input_validation";s:4:"date";}', 0, 90, NULL, 1, 1, 1, 0),
(12, 0, NULL, 0, NULL, 1, 0, NULL, 0, 0, 0, 0),
(13, 0, NULL, 0, NULL, 1, 0, NULL, 0, 0, 0, 0),
(14, 0, NULL, 0, 'a:1:{s:16:"input_validation";s:4:"date";}', 1, 0, NULL, 0, 0, 0, 0),
(15, 0, NULL, 0, NULL, 1, 0, NULL, 0, 0, 0, 0),
(16, 0, NULL, 0, NULL, 1, 0, NULL, 0, 0, 0, 0),
(17, 0, NULL, 0, 'a:1:{s:15:"max_text_length";i:255;}', 0, 100, NULL, 1, 1, 0, 1),
(18, 0, NULL, 0, NULL, 1, 0, NULL, 1, 1, 1, 0),
(19, 0, NULL, 0, NULL, 0, 0, NULL, 1, 1, 1, 0),
(20, 0, NULL, 0, 'a:0:{}', 0, 110, NULL, 1, 1, 1, 0),
(21, 1, NULL, 0, NULL, 1, 28, NULL, 0, 0, 0, 0),
(22, 0, NULL, 0, NULL, 0, 10, NULL, 0, 0, 0, 0),
(23, 1, NULL, 0, 'a:2:{s:15:"max_text_length";i:255;s:15:"min_text_length";i:1;}', 1, 20, NULL, 1, 0, 0, 1),
(24, 0, NULL, 0, NULL, 0, 30, NULL, 0, 0, 0, 0),
(25, 1, NULL, 0, 'a:2:{s:15:"max_text_length";i:255;s:15:"min_text_length";i:1;}', 1, 40, NULL, 1, 0, 0, 1),
(26, 0, NULL, 0, NULL, 0, 50, NULL, 0, 0, 0, 0),
(27, 1, NULL, 0, 'a:2:{s:15:"max_text_length";i:255;s:15:"min_text_length";i:1;}', 1, 60, NULL, 1, 0, 0, 1),
(28, 1, NULL, 2, 'a:2:{s:15:"max_text_length";i:255;s:15:"min_text_length";i:1;}', 1, 70, NULL, 1, 0, 0, 1),
(29, 1, NULL, 0, 'a:2:{s:15:"max_text_length";i:255;s:15:"min_text_length";i:1;}', 1, 80, NULL, 1, 0, 0, 1),
(30, 1, NULL, 0, NULL, 1, 90, NULL, 1, 1, 1, 0),
(31, 1, NULL, 0, NULL, 1, 100, NULL, 1, 1, 0, 1),
(32, 1, NULL, 0, NULL, 1, 100, NULL, 0, 0, 0, 0),
(33, 1, NULL, 0, 'a:0:{}', 1, 110, 'Magento\\Customer\\Model\\Attribute\\Data\\Postcode', 1, 1, 1, 1),
(34, 1, NULL, 0, 'a:2:{s:15:"max_text_length";i:255;s:15:"min_text_length";i:1;}', 1, 120, NULL, 1, 1, 1, 1),
(35, 0, NULL, 0, 'a:2:{s:15:"max_text_length";i:255;s:15:"min_text_length";i:1;}', 0, 130, NULL, 1, 0, 0, 1),
(36, 1, NULL, 0, NULL, 1, 140, NULL, 0, 0, 0, 0),
(37, 0, NULL, 0, NULL, 1, 0, NULL, 0, 0, 0, 0),
(38, 0, NULL, 0, NULL, 1, 0, NULL, 0, 0, 0, 0),
(39, 0, NULL, 0, NULL, 1, 0, NULL, 0, 0, 0, 0),
(40, 0, NULL, 0, NULL, 1, 0, NULL, 0, 0, 0, 0),
(41, 0, NULL, 0, NULL, 0, 0, NULL, 0, 0, 0, 0);

-- --------------------------------------------------------

--
-- Table structure for table `customer_eav_attribute_website`
--

CREATE TABLE `customer_eav_attribute_website` (
  `attribute_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Attribute Id',
  `website_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Website Id',
  `is_visible` smallint(5) UNSIGNED DEFAULT NULL COMMENT 'Is Visible',
  `is_required` smallint(5) UNSIGNED DEFAULT NULL COMMENT 'Is Required',
  `default_value` text COMMENT 'Default Value',
  `multiline_count` smallint(5) UNSIGNED DEFAULT NULL COMMENT 'Multiline Count'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Customer Eav Attribute Website';

--
-- Dumping data for table `customer_eav_attribute_website`
--

INSERT INTO `customer_eav_attribute_website` (`attribute_id`, `website_id`, `is_visible`, `is_required`, `default_value`, `multiline_count`) VALUES
(1, 1, NULL, NULL, NULL, NULL),
(3, 1, NULL, NULL, NULL, NULL),
(9, 1, NULL, NULL, NULL, NULL),
(10, 1, NULL, NULL, NULL, NULL),
(11, 1, NULL, NULL, NULL, NULL),
(17, 1, NULL, NULL, NULL, NULL),
(18, 1, NULL, NULL, NULL, NULL),
(19, 1, NULL, NULL, NULL, NULL),
(20, 1, NULL, NULL, NULL, NULL),
(21, 1, NULL, NULL, NULL, NULL),
(23, 1, NULL, NULL, NULL, NULL),
(25, 1, NULL, NULL, NULL, NULL),
(27, 1, NULL, NULL, NULL, NULL),
(28, 1, NULL, NULL, NULL, NULL),
(29, 1, NULL, NULL, NULL, NULL),
(30, 1, NULL, NULL, NULL, NULL),
(31, 1, NULL, NULL, NULL, NULL),
(32, 1, NULL, NULL, NULL, NULL),
(33, 1, NULL, NULL, NULL, NULL),
(34, 1, NULL, NULL, NULL, NULL),
(35, 1, NULL, NULL, NULL, NULL),
(36, 1, NULL, NULL, NULL, NULL);

-- --------------------------------------------------------

--
-- Table structure for table `customer_entity`
--

CREATE TABLE `customer_entity` (
  `entity_id` int(10) UNSIGNED NOT NULL COMMENT 'Entity Id',
  `website_id` smallint(5) UNSIGNED DEFAULT NULL COMMENT 'Website Id',
  `email` varchar(255) DEFAULT NULL COMMENT 'Email',
  `group_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Group Id',
  `increment_id` varchar(50) DEFAULT NULL COMMENT 'Increment Id',
  `store_id` smallint(5) UNSIGNED DEFAULT '0' COMMENT 'Store Id',
  `created_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT 'Created At',
  `updated_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP COMMENT 'Updated At',
  `is_active` smallint(5) UNSIGNED NOT NULL DEFAULT '1' COMMENT 'Is Active',
  `disable_auto_group_change` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Disable automatic group change based on VAT ID',
  `created_in` varchar(255) DEFAULT NULL COMMENT 'Created From',
  `prefix` varchar(40) DEFAULT NULL COMMENT 'Prefix',
  `firstname` varchar(255) DEFAULT NULL COMMENT 'First Name',
  `middlename` varchar(255) DEFAULT NULL COMMENT 'Middle Name/Initial',
  `lastname` varchar(255) DEFAULT NULL COMMENT 'Last Name',
  `suffix` varchar(40) DEFAULT NULL COMMENT 'Suffix',
  `dob` date DEFAULT NULL COMMENT 'Date Of Birth',
  `password_hash` varchar(128) DEFAULT NULL COMMENT 'Password_hash',
  `rp_token` varchar(128) DEFAULT NULL COMMENT 'Reset password token',
  `rp_token_created_at` datetime DEFAULT NULL COMMENT 'Reset password token creation time',
  `default_billing` int(10) UNSIGNED DEFAULT NULL COMMENT 'Default Billing Address',
  `default_shipping` int(10) UNSIGNED DEFAULT NULL COMMENT 'Default Shipping Address',
  `taxvat` varchar(50) DEFAULT NULL COMMENT 'Tax/VAT Number',
  `confirmation` varchar(64) DEFAULT NULL COMMENT 'Is Confirmed',
  `gender` smallint(5) UNSIGNED DEFAULT NULL COMMENT 'Gender'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Customer Entity';

--
-- Dumping data for table `customer_entity`
--

INSERT INTO `customer_entity` (`entity_id`, `website_id`, `email`, `group_id`, `increment_id`, `store_id`, `created_at`, `updated_at`, `is_active`, `disable_auto_group_change`, `created_in`, `prefix`, `firstname`, `middlename`, `lastname`, `suffix`, `dob`, `password_hash`, `rp_token`, `rp_token_created_at`, `default_billing`, `default_shipping`, `taxvat`, `confirmation`, `gender`) VALUES
(1, 1, 'lieult84@gmail.com', 1, NULL, 1, '2016-04-27 08:10:59', '2016-04-27 08:11:00', 1, 0, 'English', NULL, 'Le', NULL, 'Lieu', NULL, NULL, NULL, '71d3620101a76cd31e93852978250ab0', '2016-04-27 08:11:00', 1, NULL, NULL, NULL, NULL),
(2, 1, 'lieult84@yahoo.com', 1, NULL, 1, '2016-04-28 02:43:03', '2016-04-28 03:06:20', 1, 0, 'English', NULL, 'Le', NULL, 'Lieu', NULL, NULL, '969e71f55c60fff74a202c363cd0b89c03adfcb4138799cfd23050d0d9f8a692:UQr1PzFcoRjqbgYscEcTYSY4AAbXtPuP:1', 'cbcdef29b3a70a97d684144c91afcf44', '2016-04-28 02:43:04', 2, 2, NULL, NULL, NULL);

-- --------------------------------------------------------

--
-- Table structure for table `customer_entity_datetime`
--

CREATE TABLE `customer_entity_datetime` (
  `value_id` int(11) NOT NULL COMMENT 'Value Id',
  `attribute_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Attribute Id',
  `entity_id` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Entity Id',
  `value` datetime DEFAULT NULL COMMENT 'Value'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Customer Entity Datetime';

-- --------------------------------------------------------

--
-- Table structure for table `customer_entity_decimal`
--

CREATE TABLE `customer_entity_decimal` (
  `value_id` int(11) NOT NULL COMMENT 'Value Id',
  `attribute_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Attribute Id',
  `entity_id` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Entity Id',
  `value` decimal(12,4) NOT NULL DEFAULT '0.0000' COMMENT 'Value'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Customer Entity Decimal';

-- --------------------------------------------------------

--
-- Table structure for table `customer_entity_int`
--

CREATE TABLE `customer_entity_int` (
  `value_id` int(11) NOT NULL COMMENT 'Value Id',
  `attribute_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Attribute Id',
  `entity_id` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Entity Id',
  `value` int(11) NOT NULL DEFAULT '0' COMMENT 'Value'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Customer Entity Int';

-- --------------------------------------------------------

--
-- Table structure for table `customer_entity_text`
--

CREATE TABLE `customer_entity_text` (
  `value_id` int(11) NOT NULL COMMENT 'Value Id',
  `attribute_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Attribute Id',
  `entity_id` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Entity Id',
  `value` text NOT NULL COMMENT 'Value'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Customer Entity Text';

-- --------------------------------------------------------

--
-- Table structure for table `customer_entity_varchar`
--

CREATE TABLE `customer_entity_varchar` (
  `value_id` int(11) NOT NULL COMMENT 'Value Id',
  `attribute_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Attribute Id',
  `entity_id` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Entity Id',
  `value` varchar(255) DEFAULT NULL COMMENT 'Value'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Customer Entity Varchar';

-- --------------------------------------------------------

--
-- Table structure for table `customer_form_attribute`
--

CREATE TABLE `customer_form_attribute` (
  `form_code` varchar(32) NOT NULL COMMENT 'Form Code',
  `attribute_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Attribute Id'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Customer Form Attribute';

--
-- Dumping data for table `customer_form_attribute`
--

INSERT INTO `customer_form_attribute` (`form_code`, `attribute_id`) VALUES
('adminhtml_checkout', 9),
('adminhtml_checkout', 10),
('adminhtml_checkout', 11),
('adminhtml_checkout', 17),
('adminhtml_checkout', 20),
('adminhtml_customer', 1),
('adminhtml_customer', 3),
('adminhtml_customer', 4),
('adminhtml_customer', 5),
('adminhtml_customer', 6),
('adminhtml_customer', 7),
('adminhtml_customer', 8),
('adminhtml_customer', 9),
('adminhtml_customer', 10),
('adminhtml_customer', 11),
('adminhtml_customer', 17),
('adminhtml_customer', 19),
('adminhtml_customer', 20),
('adminhtml_customer', 21),
('adminhtml_customer_address', 22),
('adminhtml_customer_address', 23),
('adminhtml_customer_address', 24),
('adminhtml_customer_address', 25),
('adminhtml_customer_address', 26),
('adminhtml_customer_address', 27),
('adminhtml_customer_address', 28),
('adminhtml_customer_address', 29),
('adminhtml_customer_address', 30),
('adminhtml_customer_address', 31),
('adminhtml_customer_address', 32),
('adminhtml_customer_address', 33),
('adminhtml_customer_address', 34),
('adminhtml_customer_address', 35),
('adminhtml_customer_address', 36),
('customer_account_create', 4),
('customer_account_create', 5),
('customer_account_create', 6),
('customer_account_create', 7),
('customer_account_create', 8),
('customer_account_create', 9),
('customer_account_create', 11),
('customer_account_create', 17),
('customer_account_create', 19),
('customer_account_create', 20),
('customer_account_edit', 4),
('customer_account_edit', 5),
('customer_account_edit', 6),
('customer_account_edit', 7),
('customer_account_edit', 8),
('customer_account_edit', 9),
('customer_account_edit', 11),
('customer_account_edit', 17),
('customer_account_edit', 19),
('customer_account_edit', 20),
('customer_address_edit', 22),
('customer_address_edit', 23),
('customer_address_edit', 24),
('customer_address_edit', 25),
('customer_address_edit', 26),
('customer_address_edit', 27),
('customer_address_edit', 28),
('customer_address_edit', 29),
('customer_address_edit', 30),
('customer_address_edit', 31),
('customer_address_edit', 32),
('customer_address_edit', 33),
('customer_address_edit', 34),
('customer_address_edit', 35),
('customer_address_edit', 36),
('customer_register_address', 22),
('customer_register_address', 23),
('customer_register_address', 24),
('customer_register_address', 25),
('customer_register_address', 26),
('customer_register_address', 27),
('customer_register_address', 28),
('customer_register_address', 29),
('customer_register_address', 30),
('customer_register_address', 31),
('customer_register_address', 32),
('customer_register_address', 33),
('customer_register_address', 34),
('customer_register_address', 35),
('customer_register_address', 36);

-- --------------------------------------------------------

--
-- Table structure for table `customer_grid_flat`
--

CREATE TABLE `customer_grid_flat` (
  `entity_id` int(10) UNSIGNED NOT NULL COMMENT 'Entity ID',
  `name` text COMMENT 'Name',
  `email` varchar(255) DEFAULT NULL COMMENT 'Email',
  `group_id` int(11) DEFAULT NULL COMMENT 'Group_id',
  `created_at` timestamp NULL DEFAULT NULL COMMENT 'Created_at',
  `website_id` int(11) DEFAULT NULL COMMENT 'Website_id',
  `confirmation` int(11) DEFAULT NULL COMMENT 'Confirmation',
  `created_in` text COMMENT 'Created_in',
  `dob` date DEFAULT NULL COMMENT 'Dob',
  `gender` int(11) DEFAULT NULL COMMENT 'Gender',
  `taxvat` varchar(255) DEFAULT NULL COMMENT 'Taxvat',
  `last_visit_at` datetime DEFAULT NULL COMMENT 'Last_visit_at',
  `billing_full` text COMMENT 'Billing_full',
  `billing_firstname` varchar(255) DEFAULT NULL COMMENT 'Billing_firstname',
  `billing_lastname` varchar(255) DEFAULT NULL COMMENT 'Billing_lastname',
  `billing_telephone` varchar(255) DEFAULT NULL COMMENT 'Billing_telephone',
  `billing_postcode` varchar(255) DEFAULT NULL COMMENT 'Billing_postcode',
  `billing_country_id` varchar(255) DEFAULT NULL COMMENT 'Billing_country_id',
  `billing_region` varchar(255) DEFAULT NULL COMMENT 'Billing_region',
  `billing_street` varchar(255) DEFAULT NULL COMMENT 'Billing_street',
  `billing_city` varchar(255) DEFAULT NULL COMMENT 'Billing_city',
  `billing_fax` varchar(255) DEFAULT NULL COMMENT 'Billing_fax',
  `billing_vat_id` varchar(255) DEFAULT NULL COMMENT 'Billing_vat_id',
  `billing_company` varchar(255) DEFAULT NULL COMMENT 'Billing_company',
  `shipping_full` text COMMENT 'Shipping_full'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='customer_grid_flat';

--
-- Dumping data for table `customer_grid_flat`
--

INSERT INTO `customer_grid_flat` (`entity_id`, `name`, `email`, `group_id`, `created_at`, `website_id`, `confirmation`, `created_in`, `dob`, `gender`, `taxvat`, `last_visit_at`, `billing_full`, `billing_firstname`, `billing_lastname`, `billing_telephone`, `billing_postcode`, `billing_country_id`, `billing_region`, `billing_street`, `billing_city`, `billing_fax`, `billing_vat_id`, `billing_company`, `shipping_full`) VALUES
(1, 'Le Lieu', 'lieult84@gmail.com', 1, '2016-04-27 08:10:59', 1, NULL, 'English', NULL, NULL, NULL, NULL, 'MD Ha Noi Alabama 12345', 'Le', 'Lieu', '123456789', '12345', 'US', 'Alabama', 'MD', 'Ha Noi', NULL, NULL, 'Brainos', ''),
(2, 'Le Lieu', 'lieult84@yahoo.com', 1, '2016-04-28 02:43:03', 1, NULL, 'English', NULL, NULL, NULL, '2016-04-28 04:33:54', 'MD Ha Noi Alabama 12345', 'Le', 'Lieu', '123456789', '12345', 'US', 'Alabama', 'MD', 'Ha Noi', NULL, NULL, 'TNT', 'MD Ha Noi Alabama 12345');

-- --------------------------------------------------------

--
-- Table structure for table `customer_group`
--

CREATE TABLE `customer_group` (
  `customer_group_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Customer Group Id',
  `customer_group_code` varchar(32) NOT NULL COMMENT 'Customer Group Code',
  `tax_class_id` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Tax Class Id'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Customer Group';

--
-- Dumping data for table `customer_group`
--

INSERT INTO `customer_group` (`customer_group_id`, `customer_group_code`, `tax_class_id`) VALUES
(0, 'NOT LOGGED IN', 3),
(1, 'General', 3),
(2, 'Wholesale', 3),
(3, 'Retailer', 3);

-- --------------------------------------------------------

--
-- Table structure for table `customer_log`
--

CREATE TABLE `customer_log` (
  `log_id` int(11) NOT NULL COMMENT 'Log ID',
  `customer_id` int(11) NOT NULL COMMENT 'Customer ID',
  `last_login_at` timestamp NULL DEFAULT NULL COMMENT 'Last Login Time',
  `last_logout_at` timestamp NULL DEFAULT NULL COMMENT 'Last Logout Time'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Customer Log Table';

--
-- Dumping data for table `customer_log`
--

INSERT INTO `customer_log` (`log_id`, `customer_id`, `last_login_at`, `last_logout_at`) VALUES
(1, 2, '2016-04-29 09:43:38', NULL);

-- --------------------------------------------------------

--
-- Table structure for table `customer_visitor`
--

CREATE TABLE `customer_visitor` (
  `visitor_id` bigint(20) UNSIGNED NOT NULL COMMENT 'Visitor ID',
  `customer_id` int(11) DEFAULT NULL COMMENT 'Customer Id',
  `session_id` varchar(64) DEFAULT NULL COMMENT 'Session ID',
  `last_visit_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP COMMENT 'Last Visit Time'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Visitor Table';

--
-- Dumping data for table `customer_visitor`
--

INSERT INTO `customer_visitor` (`visitor_id`, `customer_id`, `session_id`, `last_visit_at`) VALUES
(1, NULL, 'gjokin3ktfc8vt9kmijkl6f4j0', '2016-04-12 15:11:44'),
(2, NULL, 's1q7qvbrlfc40hasn6i3h8a3j2', '2016-04-12 15:25:50'),
(3, NULL, 'luqmc8k07piamenbd8b5q6gsl1', '2016-04-13 00:05:49'),
(4, NULL, 'm4tu9ukf2296iifo7kmo52fbp4', '2016-04-14 14:05:04'),
(5, NULL, 'h31q17bqbpvd2kse28s6neg8u5', '2016-04-14 14:38:38'),
(6, NULL, '4t00lvfsvvkdntlgcaho1e7lq0', '2016-04-15 03:14:27'),
(7, NULL, 'utmf852oncsaq9qai5jq9gjm00', '2016-04-15 04:24:45'),
(8, NULL, 'k5c8ndn30q5hl2ehhi62pce190', '2016-04-15 04:29:45'),
(9, NULL, 'ktrq1j1ra8b9c7gt5dqssf0565', '2016-04-15 04:58:41'),
(10, NULL, 'okrcpq1cbs2l4sphf19uudvf75', '2016-04-15 07:34:26'),
(11, NULL, '7bujd9tptjqafcfedq9nkfd2v7', '2016-04-15 07:09:51'),
(12, NULL, 'vki3dg7jrfonai0pmg16v54247', '2016-04-15 07:10:06'),
(13, NULL, 'fuha0phd8frl0jif9vpivm5170', '2016-04-15 08:03:47'),
(14, NULL, 'el0cfbgut2s5e1ldsnihvs2063', '2016-04-15 07:10:06'),
(15, NULL, 'aulql8n1bs4j0enlq21a3o79s2', '2016-04-15 08:11:35'),
(16, NULL, 'qo06dmf5dn176qeslertnn7c76', '2016-04-15 08:45:48'),
(17, NULL, 'qbboosnc82nurhauspgsujs8n3', '2016-04-15 08:33:13'),
(18, NULL, '9cl00762k5p22qjt511h7vmfv5', '2016-04-15 09:16:45'),
(19, NULL, '8lv0tkjqfcsamn6vav68poa7p2', '2016-04-15 09:40:28'),
(20, NULL, 'i7p49afvifl4f1139qsrtv35s6', '2016-04-15 09:57:22'),
(21, NULL, '0u0akmflg4m1puv03evm4ah432', '2016-04-15 10:27:24'),
(22, NULL, '4an5pmqtaamtnq2ran1pge6374', '2016-04-15 10:35:57'),
(23, NULL, 'v7qdsk4m7pbb2sgshcj7kohtm0', '2016-04-15 15:54:18'),
(24, NULL, 'brn84nk6832hpon8oojhard7g0', '2016-04-16 02:27:21'),
(25, NULL, 'm3k462srtcu6ms68jefkj7sle2', '2016-04-16 02:52:35'),
(26, NULL, 'o6phgcf8vihaakqkuh86jqaq17', '2016-04-16 03:18:39'),
(27, NULL, '42ofvefb0m8eubuiiktme4r6n4', '2016-04-17 14:43:16'),
(28, NULL, 'j53jk5k3i0ud5npdevac12m7e6', '2016-04-18 02:16:01'),
(29, NULL, '8mjsac0425mpr0f6e2fh9320l7', '2016-04-18 03:03:36'),
(30, NULL, 'kq4r545g3geuq9ve9vruv9m8i1', '2016-04-18 02:36:54'),
(31, NULL, 'fq8lf137med4deuj2fclpr4lv3', '2016-04-18 03:37:03'),
(32, NULL, 'edmi7jfm78q3910cpr9dp8vie0', '2016-04-18 04:06:31'),
(33, NULL, 'bpvbjdb4l75svbtu2pbrhkfas2', '2016-04-18 04:45:57'),
(34, NULL, 'sve1u6dgro9mj2pfig0uj0l6j0', '2016-04-18 04:53:38'),
(35, NULL, 'rrcm11740810dk8mgvs9qiqhs1', '2016-04-18 05:01:51'),
(36, NULL, 'ivftl9j2kvi31hbmpvam2ftda6', '2016-04-18 07:16:28'),
(37, NULL, 'ip19ms00s38qmlka89j2i5jam1', '2016-04-18 07:34:48'),
(38, NULL, 'v0hgkafbc54lktji970fa610f4', '2016-04-18 08:11:23'),
(39, NULL, 'l3bct1t2tbmvdm42bhpp4uld53', '2016-04-18 07:37:44'),
(40, NULL, 'ncv7rrjfvsrokp3gqc6qlf0lp4', '2016-04-18 07:37:44'),
(41, NULL, '9p6l24oekt4jg13bu94a5c12t4', '2016-04-18 08:27:39'),
(42, NULL, 'nfnv1p40crfku37l1n14sbca85', '2016-04-18 09:23:21'),
(43, NULL, 'kd1fj6ecuvd60ehpbeed2kfav5', '2016-04-18 08:34:23'),
(44, NULL, 'aumfgn5khntbrjccp84d0h6js4', '2016-04-18 09:33:54'),
(45, NULL, 's607blfr9ugc7u6nvpcuaptkk2', '2016-04-18 10:32:14'),
(46, NULL, '5990j9emd2hfuggs32ombqp987', '2016-04-18 10:04:43'),
(47, NULL, 'k0mhtv2triglijfbu6og78u9r3', '2016-04-18 10:32:36'),
(48, NULL, 'cf10r4d3766d7llttjsdiimbq6', '2016-04-18 10:34:31'),
(49, NULL, 'n29e4ra266pdg189t843q21ma5', '2016-04-19 01:52:41'),
(50, NULL, 'u8mlsd08o9q7r2ru7jo4aqomv2', '2016-04-19 03:57:03'),
(51, NULL, 'o4r6rvc7c3dvvdeveesem6cae1', '2016-04-19 04:34:46'),
(52, NULL, 'qi7bpisi81bgfmg4rucat6usg1', '2016-04-19 04:35:02'),
(53, NULL, 'dned4vddp9jmbcp6ad98j66dv5', '2016-04-19 04:34:47'),
(54, NULL, 't0dii0acck3fki2phjucja15e7', '2016-04-19 06:52:34'),
(55, NULL, 'qtsefklrrtkdvf4fvc8emsjul3', '2016-04-19 07:17:12'),
(56, NULL, 'iieqdcidt8ld1vk3e2qtpemir3', '2016-04-19 06:52:34'),
(57, NULL, 'c9t3bhkku8t4fu40tsba52t9l6', '2016-04-19 07:54:26'),
(58, NULL, '37jdge7sl838lhsqg26e398j33', '2016-04-19 09:09:20'),
(59, NULL, '8dgj5naafbe3dk4rp30de31fb3', '2016-04-19 08:19:59'),
(60, NULL, 'tr0jp0hu0gc23b3s3u1hv2ioi1', '2016-04-19 09:15:19'),
(61, NULL, 'fbb3p3t96pbb49dodngv53bnn4', '2016-04-19 09:15:19'),
(62, NULL, '7nbhi3s5o917npv1f70o0rusp3', '2016-04-19 09:44:43'),
(63, NULL, '8c14n6292lvpkmsrt9ug3p7512', '2016-04-19 09:37:16'),
(64, NULL, 'cbarcs1rsuvn17nc3mige4bof5', '2016-04-20 03:09:03'),
(65, NULL, 'rne7rj8uslsppdcji8d7o5icm6', '2016-04-20 03:15:39'),
(66, NULL, '8fq79v9cck10934jn34s4i7s63', '2016-04-20 03:17:05'),
(67, NULL, 'hov7ul9q72fd890hkko4l2sip2', '2016-04-20 04:13:29'),
(68, NULL, 'ikpdlhnf46uaidduhujll915r4', '2016-04-20 04:55:15'),
(69, NULL, 'lqnf7teups30n65p4rhpcbm5c3', '2016-04-20 07:41:07'),
(70, NULL, 'aqd7r0qurnanhvl41rklffel97', '2016-04-20 07:56:09'),
(71, NULL, 'bqoa4nih91qhafl0f69rfmncc7', '2016-04-20 08:42:36'),
(72, NULL, 'cvdkp7afbe3jpbg1qav7ff1pk7', '2016-04-20 09:00:38'),
(73, NULL, '9a2get8f9vbk18navqu47ek604', '2016-04-20 08:49:03'),
(74, NULL, 'dqlo13kvoprlbt55hdmrp65t57', '2016-04-20 09:36:14'),
(75, NULL, 'o75trg71daa3416fv2pdls8ot7', '2016-04-20 09:01:13'),
(76, NULL, 'da2468aekc45jgenrltvscjbj5', '2016-04-20 09:46:40'),
(77, NULL, 'jcgkuglvshskv5lcujrf9lihp6', '2016-04-20 10:13:01'),
(78, NULL, 'dlqrs8noa7a3cfgmdgnp1kmgi1', '2016-04-21 02:29:08'),
(79, NULL, 'j55502vhgk6iku1iofauprl9f0', '2016-04-21 03:39:50'),
(80, NULL, 'drccagku9umv69tvh40ubvsin2', '2016-04-21 03:40:45'),
(81, NULL, '7qhb131hjb0ekf0sbq10qaqt71', '2016-04-21 03:40:46'),
(82, NULL, 'oonugltif8k21jdnuipn9tg647', '2016-04-21 03:49:37'),
(83, NULL, 'kafbr7gjqqkvnjm01tthfrr9k5', '2016-04-21 04:40:12'),
(84, NULL, 't4ndvs2dcel7lv8t5gomhbkvm4', '2016-04-21 04:42:06'),
(85, NULL, 'a56jgn3e5ulhekb2tmt04kcgq1', '2016-04-21 04:42:07'),
(86, NULL, 'h7u6669l09h07n66jalk7q1m84', '2016-04-21 04:42:07'),
(87, NULL, 'o86c87qq9265uogk0r3165r2s1', '2016-04-21 04:44:42'),
(88, NULL, 'dm7gg7bsuh09g64f82lhnq7e94', '2016-04-21 04:58:27'),
(89, NULL, '2ckvca9fco4n5jibsee127v335', '2016-04-21 06:42:15'),
(90, NULL, 'k7o3ji023l9omk8g6r0e33d5b2', '2016-04-21 06:42:08'),
(91, NULL, 'ikhnpuc5snergrerlt8j2ggq55', '2016-04-21 06:42:23'),
(92, NULL, 'eni3900aq9s7akueh08vhvnig2', '2016-04-21 06:52:26'),
(93, NULL, '5m0r18l34ngujvoo4hogd91cf7', '2016-04-21 06:52:50'),
(94, NULL, 'ks22j52ennovfs0oj6i8d65m65', '2016-04-21 06:55:58'),
(95, NULL, '9ngplvestq1qoj4u528boo6ec4', '2016-04-21 07:50:08'),
(96, NULL, 'rnn5esqsg0hl9d3ufdo1epdav4', '2016-04-21 06:56:06'),
(97, NULL, 'j8t2mgd627d5lpi0o5j3jqt4j0', '2016-04-21 10:15:50'),
(98, NULL, 'i0r4jfrfosombk5t0fkjeanvd7', '2016-04-22 08:11:34'),
(99, NULL, '7ocl237shrf4vi26c8smm47np4', '2016-04-22 09:11:28'),
(100, NULL, 'l6975rsufhigislb8romkl8604', '2016-04-22 09:54:38'),
(101, NULL, 'kmu714konoroebs4nv7luo6vm0', '2016-04-22 09:54:39'),
(102, NULL, 'p3957g2bqjup2nmujdr2j7t3p3', '2016-04-22 10:03:03'),
(103, NULL, 'vn6v7fkhta7pdid6f2rq4832l1', '2016-04-23 01:52:41'),
(104, NULL, 'q4j1ql9cvk3tlp6t8v2scm8s50', '2016-04-23 01:57:42'),
(105, NULL, '8qdm55nr3llkh4mo280a7cbgj5', '2016-04-23 02:15:48'),
(106, NULL, '2g5tlvg8v5qbrkds52efbdo2d0', '2016-04-23 02:51:41'),
(107, NULL, 'emkm4jlhd94u9o05pnb2v79ck1', '2016-04-23 03:39:49'),
(108, NULL, 'jsan9sgdgiouo2nff2najt8th6', '2016-04-23 04:39:32'),
(109, NULL, 'n4b9gvmt31ui84kgmcp8uqrsd6', '2016-04-23 04:45:22'),
(110, NULL, '7odj0gr1nl21c59m1dofe22a82', '2016-04-23 04:43:17'),
(111, NULL, 'q6s4fbf982495inu5eu5iaeha5', '2016-04-23 04:39:39'),
(112, NULL, '6fcbi4utpkito7baoplg248ar6', '2016-04-23 07:53:42'),
(113, NULL, 'htfbiasu2rfcr45qu7p3vfi6s1', '2016-04-23 07:46:25'),
(114, NULL, 'ntah72bc93man90rl1shm6u346', '2016-04-23 08:13:01'),
(115, NULL, '73414pldas27etv9gpbok1d933', '2016-04-23 09:11:48'),
(116, NULL, 'lfjcefp3dbmclqha87qm8jiof6', '2016-04-23 09:18:53'),
(117, NULL, 'bmgge0hqc0mf78390b1hbl9nh5', '2016-04-23 09:58:53'),
(118, NULL, 'g1fo3kdjca2717g4ebjab33bg0', '2016-04-25 02:03:39'),
(119, NULL, 'jji2mffoqh5bejb226g14mj3o3', '2016-04-25 03:01:33'),
(120, NULL, '9h2rsbnkqgfqfki4qnlks3li53', '2016-04-25 02:55:00'),
(121, NULL, 'udq7p3qolldledrdqaqijv8650', '2016-04-25 03:11:58'),
(122, NULL, 'atvl4i47bdof718vburn8ucef5', '2016-04-25 03:14:25'),
(123, NULL, 'f3ut4p6tqse13hsdf0v7ivo455', '2016-04-25 03:19:58'),
(124, NULL, 'nsfdpeiref3nttsl4vk8up8md5', '2016-04-25 04:20:04'),
(125, NULL, 't9vt5d0f121k77pspqohpabtf4', '2016-04-25 04:32:59'),
(126, NULL, 'dbdhg4fvvi0l7usir4tpbe59e3', '2016-04-25 04:34:19'),
(127, NULL, 'muci583sfu7vm2bv4d9i9b7s46', '2016-04-25 07:21:08'),
(128, NULL, 'k78ad4bkih7ppqc0fnt8iqdau0', '2016-04-25 10:23:56'),
(129, NULL, '0gqavn1ctcutlpaj2fcr6pr154', '2016-04-25 10:34:57'),
(130, NULL, '918hn8oh8updki76c43u70k5s2', '2016-04-27 02:35:45'),
(131, NULL, 'jvpodsi54ok8merhjun1lud0j1', '2016-04-27 02:55:35'),
(132, NULL, '8hf8shuqhil2qqf6i8hii6vii6', '2016-04-27 02:59:04'),
(133, NULL, 'ljqetfkuhpgjb04u8r9r4tajq3', '2016-04-27 03:57:53'),
(134, NULL, 'vbeactpi8ralogaa8juj2ggoe0', '2016-04-27 03:13:44'),
(135, NULL, 'ibm4uqnjb547av916oru8kiea3', '2016-04-27 04:36:07'),
(136, NULL, 'eaf4crk6ef5aaenfjk8m60c290', '2016-04-27 04:42:34'),
(137, NULL, 'mumc603ch5oovt58kjrgl7jfc1', '2016-04-27 07:41:22'),
(138, NULL, 'nojruulh8jrr38s3a3p491tbv7', '2016-04-27 07:43:31'),
(139, NULL, 'pdesn5q3i66o4qfimp0831get7', '2016-04-27 07:45:51'),
(140, NULL, 'ms0r84mr5178iuncgh8doh0ic3', '2016-04-27 08:24:06'),
(141, NULL, 'lm4qtlehgtffqpje9rrbvpegp7', '2016-04-27 08:14:12'),
(142, NULL, 'ms0r84mr5178iuncgh8doh0ic3', '2016-04-27 08:08:59'),
(143, NULL, '9t3i69osgeor64fljg8cgb1c24', '2016-04-27 09:56:48'),
(144, NULL, 'i0b5gpopjnbf5b4go4tl99k3g0', '2016-04-28 02:32:54'),
(145, 2, 'mri224cgl8bsc7tm3qm7iaafv1', '2016-04-28 03:08:48'),
(146, 2, 'srl1n2v68sep6sb01onumvq781', '2016-04-28 03:15:19'),
(147, 2, '3jv2bn01ahvee1qkq82ii29db5', '2016-04-28 04:33:54'),
(148, 2, '7essosgobnan3e31ko4plstl21', '2016-04-28 04:12:39'),
(149, NULL, 'qndr830bpmcgsbf9srd3vkese3', '2016-04-29 02:21:24'),
(150, NULL, '6qiv31u1r1uvn8vb27e58ofd46', '2016-04-29 03:43:34'),
(151, NULL, '2imu8p8dsk1kkc2tjen7sbl336', '2016-04-29 04:39:27'),
(152, NULL, 'u5bj0ndtm0fg472n3heqttmk96', '2016-04-29 03:47:52'),
(153, NULL, 'h0tpa5ss86sgbqti4qseifh0l7', '2016-04-29 03:48:39'),
(154, NULL, 'ofd6938jporfbihfbg938nj4n5', '2016-04-29 03:59:56'),
(155, NULL, '9eaqjv8f291j0o4uq5hpm0vu50', '2016-04-29 04:43:31'),
(156, NULL, '16ok4kaqnke3um80si4fh81503', '2016-04-29 05:01:47'),
(157, NULL, '42r7245v10q5k0b48m2hu6big5', '2016-04-29 07:42:15'),
(158, 2, 's0iq5cgkau3ascm7hqdb9j9ca1', '2016-04-29 09:04:20'),
(159, NULL, 'bk3amg9f2ev7a36r1jcb4ljvj7', '2016-04-29 08:48:39'),
(160, NULL, '9ajin01ujllld3r7u1u31bt4k3', '2016-04-29 08:58:39'),
(161, 2, '4moemtmpia5iuebc1r3rhkkiv5', '2016-04-29 10:01:45');

-- --------------------------------------------------------

--
-- Table structure for table `design_change`
--

CREATE TABLE `design_change` (
  `design_change_id` int(11) NOT NULL COMMENT 'Design Change Id',
  `store_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Store Id',
  `design` varchar(255) DEFAULT NULL COMMENT 'Design',
  `date_from` date DEFAULT NULL COMMENT 'First Date of Design Activity',
  `date_to` date DEFAULT NULL COMMENT 'Last Date of Design Activity'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Design Changes';

-- --------------------------------------------------------

--
-- Table structure for table `directory_country`
--

CREATE TABLE `directory_country` (
  `country_id` varchar(2) NOT NULL COMMENT 'Country Id in ISO-2',
  `iso2_code` varchar(2) DEFAULT NULL COMMENT 'Country ISO-2 format',
  `iso3_code` varchar(3) DEFAULT NULL COMMENT 'Country ISO-3'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Directory Country';

--
-- Dumping data for table `directory_country`
--

INSERT INTO `directory_country` (`country_id`, `iso2_code`, `iso3_code`) VALUES
('AD', 'AD', 'AND'),
('AE', 'AE', 'ARE'),
('AF', 'AF', 'AFG'),
('AG', 'AG', 'ATG'),
('AI', 'AI', 'AIA'),
('AL', 'AL', 'ALB'),
('AM', 'AM', 'ARM'),
('AN', 'AN', 'ANT'),
('AO', 'AO', 'AGO'),
('AQ', 'AQ', 'ATA'),
('AR', 'AR', 'ARG'),
('AS', 'AS', 'ASM'),
('AT', 'AT', 'AUT'),
('AU', 'AU', 'AUS'),
('AW', 'AW', 'ABW'),
('AX', 'AX', 'ALA'),
('AZ', 'AZ', 'AZE'),
('BA', 'BA', 'BIH'),
('BB', 'BB', 'BRB'),
('BD', 'BD', 'BGD'),
('BE', 'BE', 'BEL'),
('BF', 'BF', 'BFA'),
('BG', 'BG', 'BGR'),
('BH', 'BH', 'BHR'),
('BI', 'BI', 'BDI'),
('BJ', 'BJ', 'BEN'),
('BL', 'BL', 'BLM'),
('BM', 'BM', 'BMU'),
('BN', 'BN', 'BRN'),
('BO', 'BO', 'BOL'),
('BR', 'BR', 'BRA'),
('BS', 'BS', 'BHS'),
('BT', 'BT', 'BTN'),
('BV', 'BV', 'BVT'),
('BW', 'BW', 'BWA'),
('BY', 'BY', 'BLR'),
('BZ', 'BZ', 'BLZ'),
('CA', 'CA', 'CAN'),
('CC', 'CC', 'CCK'),
('CD', 'CD', 'COD'),
('CF', 'CF', 'CAF'),
('CG', 'CG', 'COG'),
('CH', 'CH', 'CHE'),
('CI', 'CI', 'CIV'),
('CK', 'CK', 'COK'),
('CL', 'CL', 'CHL'),
('CM', 'CM', 'CMR'),
('CN', 'CN', 'CHN'),
('CO', 'CO', 'COL'),
('CR', 'CR', 'CRI'),
('CU', 'CU', 'CUB'),
('CV', 'CV', 'CPV'),
('CX', 'CX', 'CXR'),
('CY', 'CY', 'CYP'),
('CZ', 'CZ', 'CZE'),
('DE', 'DE', 'DEU'),
('DJ', 'DJ', 'DJI'),
('DK', 'DK', 'DNK'),
('DM', 'DM', 'DMA'),
('DO', 'DO', 'DOM'),
('DZ', 'DZ', 'DZA'),
('EC', 'EC', 'ECU'),
('EE', 'EE', 'EST'),
('EG', 'EG', 'EGY'),
('EH', 'EH', 'ESH'),
('ER', 'ER', 'ERI'),
('ES', 'ES', 'ESP'),
('ET', 'ET', 'ETH'),
('FI', 'FI', 'FIN'),
('FJ', 'FJ', 'FJI'),
('FK', 'FK', 'FLK'),
('FM', 'FM', 'FSM'),
('FO', 'FO', 'FRO'),
('FR', 'FR', 'FRA'),
('GA', 'GA', 'GAB'),
('GB', 'GB', 'GBR'),
('GD', 'GD', 'GRD'),
('GE', 'GE', 'GEO'),
('GF', 'GF', 'GUF'),
('GG', 'GG', 'GGY'),
('GH', 'GH', 'GHA'),
('GI', 'GI', 'GIB'),
('GL', 'GL', 'GRL'),
('GM', 'GM', 'GMB'),
('GN', 'GN', 'GIN'),
('GP', 'GP', 'GLP'),
('GQ', 'GQ', 'GNQ'),
('GR', 'GR', 'GRC'),
('GS', 'GS', 'SGS'),
('GT', 'GT', 'GTM'),
('GU', 'GU', 'GUM'),
('GW', 'GW', 'GNB'),
('GY', 'GY', 'GUY'),
('HK', 'HK', 'HKG'),
('HM', 'HM', 'HMD'),
('HN', 'HN', 'HND'),
('HR', 'HR', 'HRV'),
('HT', 'HT', 'HTI'),
('HU', 'HU', 'HUN'),
('ID', 'ID', 'IDN'),
('IE', 'IE', 'IRL'),
('IL', 'IL', 'ISR'),
('IM', 'IM', 'IMN'),
('IN', 'IN', 'IND'),
('IO', 'IO', 'IOT'),
('IQ', 'IQ', 'IRQ'),
('IR', 'IR', 'IRN'),
('IS', 'IS', 'ISL'),
('IT', 'IT', 'ITA'),
('JE', 'JE', 'JEY'),
('JM', 'JM', 'JAM'),
('JO', 'JO', 'JOR'),
('JP', 'JP', 'JPN'),
('KE', 'KE', 'KEN'),
('KG', 'KG', 'KGZ'),
('KH', 'KH', 'KHM'),
('KI', 'KI', 'KIR'),
('KM', 'KM', 'COM'),
('KN', 'KN', 'KNA'),
('KP', 'KP', 'PRK'),
('KR', 'KR', 'KOR'),
('KW', 'KW', 'KWT'),
('KY', 'KY', 'CYM'),
('KZ', 'KZ', 'KAZ'),
('LA', 'LA', 'LAO'),
('LB', 'LB', 'LBN'),
('LC', 'LC', 'LCA'),
('LI', 'LI', 'LIE'),
('LK', 'LK', 'LKA'),
('LR', 'LR', 'LBR'),
('LS', 'LS', 'LSO'),
('LT', 'LT', 'LTU'),
('LU', 'LU', 'LUX'),
('LV', 'LV', 'LVA'),
('LY', 'LY', 'LBY'),
('MA', 'MA', 'MAR'),
('MC', 'MC', 'MCO'),
('MD', 'MD', 'MDA'),
('ME', 'ME', 'MNE'),
('MF', 'MF', 'MAF'),
('MG', 'MG', 'MDG'),
('MH', 'MH', 'MHL'),
('MK', 'MK', 'MKD'),
('ML', 'ML', 'MLI'),
('MM', 'MM', 'MMR'),
('MN', 'MN', 'MNG'),
('MO', 'MO', 'MAC'),
('MP', 'MP', 'MNP'),
('MQ', 'MQ', 'MTQ'),
('MR', 'MR', 'MRT'),
('MS', 'MS', 'MSR'),
('MT', 'MT', 'MLT'),
('MU', 'MU', 'MUS'),
('MV', 'MV', 'MDV'),
('MW', 'MW', 'MWI'),
('MX', 'MX', 'MEX'),
('MY', 'MY', 'MYS'),
('MZ', 'MZ', 'MOZ'),
('NA', 'NA', 'NAM'),
('NC', 'NC', 'NCL'),
('NE', 'NE', 'NER'),
('NF', 'NF', 'NFK'),
('NG', 'NG', 'NGA'),
('NI', 'NI', 'NIC'),
('NL', 'NL', 'NLD'),
('NO', 'NO', 'NOR'),
('NP', 'NP', 'NPL'),
('NR', 'NR', 'NRU'),
('NU', 'NU', 'NIU'),
('NZ', 'NZ', 'NZL'),
('OM', 'OM', 'OMN'),
('PA', 'PA', 'PAN'),
('PE', 'PE', 'PER'),
('PF', 'PF', 'PYF'),
('PG', 'PG', 'PNG'),
('PH', 'PH', 'PHL'),
('PK', 'PK', 'PAK'),
('PL', 'PL', 'POL'),
('PM', 'PM', 'SPM'),
('PN', 'PN', 'PCN'),
('PS', 'PS', 'PSE'),
('PT', 'PT', 'PRT'),
('PW', 'PW', 'PLW'),
('PY', 'PY', 'PRY'),
('QA', 'QA', 'QAT'),
('RE', 'RE', 'REU'),
('RO', 'RO', 'ROU'),
('RS', 'RS', 'SRB'),
('RU', 'RU', 'RUS'),
('RW', 'RW', 'RWA'),
('SA', 'SA', 'SAU'),
('SB', 'SB', 'SLB'),
('SC', 'SC', 'SYC'),
('SD', 'SD', 'SDN'),
('SE', 'SE', 'SWE'),
('SG', 'SG', 'SGP'),
('SH', 'SH', 'SHN'),
('SI', 'SI', 'SVN'),
('SJ', 'SJ', 'SJM'),
('SK', 'SK', 'SVK'),
('SL', 'SL', 'SLE'),
('SM', 'SM', 'SMR'),
('SN', 'SN', 'SEN'),
('SO', 'SO', 'SOM'),
('SR', 'SR', 'SUR'),
('ST', 'ST', 'STP'),
('SV', 'SV', 'SLV'),
('SY', 'SY', 'SYR'),
('SZ', 'SZ', 'SWZ'),
('TC', 'TC', 'TCA'),
('TD', 'TD', 'TCD'),
('TF', 'TF', 'ATF'),
('TG', 'TG', 'TGO'),
('TH', 'TH', 'THA'),
('TJ', 'TJ', 'TJK'),
('TK', 'TK', 'TKL'),
('TL', 'TL', 'TLS'),
('TM', 'TM', 'TKM'),
('TN', 'TN', 'TUN'),
('TO', 'TO', 'TON'),
('TR', 'TR', 'TUR'),
('TT', 'TT', 'TTO'),
('TV', 'TV', 'TUV'),
('TW', 'TW', 'TWN'),
('TZ', 'TZ', 'TZA'),
('UA', 'UA', 'UKR'),
('UG', 'UG', 'UGA'),
('UM', 'UM', 'UMI'),
('US', 'US', 'USA'),
('UY', 'UY', 'URY'),
('UZ', 'UZ', 'UZB'),
('VA', 'VA', 'VAT'),
('VC', 'VC', 'VCT'),
('VE', 'VE', 'VEN'),
('VG', 'VG', 'VGB'),
('VI', 'VI', 'VIR'),
('VN', 'VN', 'VNM'),
('VU', 'VU', 'VUT'),
('WF', 'WF', 'WLF'),
('WS', 'WS', 'WSM'),
('YE', 'YE', 'YEM'),
('YT', 'YT', 'MYT'),
('ZA', 'ZA', 'ZAF'),
('ZM', 'ZM', 'ZMB'),
('ZW', 'ZW', 'ZWE');

-- --------------------------------------------------------

--
-- Table structure for table `directory_country_format`
--

CREATE TABLE `directory_country_format` (
  `country_format_id` int(10) UNSIGNED NOT NULL COMMENT 'Country Format Id',
  `country_id` varchar(2) DEFAULT NULL COMMENT 'Country Id in ISO-2',
  `type` varchar(30) DEFAULT NULL COMMENT 'Country Format Type',
  `format` text NOT NULL COMMENT 'Country Format'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Directory Country Format';

-- --------------------------------------------------------

--
-- Table structure for table `directory_country_region`
--

CREATE TABLE `directory_country_region` (
  `region_id` int(10) UNSIGNED NOT NULL COMMENT 'Region Id',
  `country_id` varchar(4) NOT NULL DEFAULT '0' COMMENT 'Country Id in ISO-2',
  `code` varchar(32) DEFAULT NULL COMMENT 'Region code',
  `default_name` varchar(255) DEFAULT NULL COMMENT 'Region Name'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Directory Country Region';

--
-- Dumping data for table `directory_country_region`
--

INSERT INTO `directory_country_region` (`region_id`, `country_id`, `code`, `default_name`) VALUES
(1, 'US', 'AL', 'Alabama'),
(2, 'US', 'AK', 'Alaska'),
(3, 'US', 'AS', 'American Samoa'),
(4, 'US', 'AZ', 'Arizona'),
(5, 'US', 'AR', 'Arkansas'),
(6, 'US', 'AE', 'Armed Forces Africa'),
(7, 'US', 'AA', 'Armed Forces Americas'),
(8, 'US', 'AE', 'Armed Forces Canada'),
(9, 'US', 'AE', 'Armed Forces Europe'),
(10, 'US', 'AE', 'Armed Forces Middle East'),
(11, 'US', 'AP', 'Armed Forces Pacific'),
(12, 'US', 'CA', 'California'),
(13, 'US', 'CO', 'Colorado'),
(14, 'US', 'CT', 'Connecticut'),
(15, 'US', 'DE', 'Delaware'),
(16, 'US', 'DC', 'District of Columbia'),
(17, 'US', 'FM', 'Federated States Of Micronesia'),
(18, 'US', 'FL', 'Florida'),
(19, 'US', 'GA', 'Georgia'),
(20, 'US', 'GU', 'Guam'),
(21, 'US', 'HI', 'Hawaii'),
(22, 'US', 'ID', 'Idaho'),
(23, 'US', 'IL', 'Illinois'),
(24, 'US', 'IN', 'Indiana'),
(25, 'US', 'IA', 'Iowa'),
(26, 'US', 'KS', 'Kansas'),
(27, 'US', 'KY', 'Kentucky'),
(28, 'US', 'LA', 'Louisiana'),
(29, 'US', 'ME', 'Maine'),
(30, 'US', 'MH', 'Marshall Islands'),
(31, 'US', 'MD', 'Maryland'),
(32, 'US', 'MA', 'Massachusetts'),
(33, 'US', 'MI', 'Michigan'),
(34, 'US', 'MN', 'Minnesota'),
(35, 'US', 'MS', 'Mississippi'),
(36, 'US', 'MO', 'Missouri'),
(37, 'US', 'MT', 'Montana'),
(38, 'US', 'NE', 'Nebraska'),
(39, 'US', 'NV', 'Nevada'),
(40, 'US', 'NH', 'New Hampshire'),
(41, 'US', 'NJ', 'New Jersey'),
(42, 'US', 'NM', 'New Mexico'),
(43, 'US', 'NY', 'New York'),
(44, 'US', 'NC', 'North Carolina'),
(45, 'US', 'ND', 'North Dakota'),
(46, 'US', 'MP', 'Northern Mariana Islands'),
(47, 'US', 'OH', 'Ohio'),
(48, 'US', 'OK', 'Oklahoma'),
(49, 'US', 'OR', 'Oregon'),
(50, 'US', 'PW', 'Palau'),
(51, 'US', 'PA', 'Pennsylvania'),
(52, 'US', 'PR', 'Puerto Rico'),
(53, 'US', 'RI', 'Rhode Island'),
(54, 'US', 'SC', 'South Carolina'),
(55, 'US', 'SD', 'South Dakota'),
(56, 'US', 'TN', 'Tennessee'),
(57, 'US', 'TX', 'Texas'),
(58, 'US', 'UT', 'Utah'),
(59, 'US', 'VT', 'Vermont'),
(60, 'US', 'VI', 'Virgin Islands'),
(61, 'US', 'VA', 'Virginia'),
(62, 'US', 'WA', 'Washington'),
(63, 'US', 'WV', 'West Virginia'),
(64, 'US', 'WI', 'Wisconsin'),
(65, 'US', 'WY', 'Wyoming'),
(66, 'CA', 'AB', 'Alberta'),
(67, 'CA', 'BC', 'British Columbia'),
(68, 'CA', 'MB', 'Manitoba'),
(69, 'CA', 'NL', 'Newfoundland and Labrador'),
(70, 'CA', 'NB', 'New Brunswick'),
(71, 'CA', 'NS', 'Nova Scotia'),
(72, 'CA', 'NT', 'Northwest Territories'),
(73, 'CA', 'NU', 'Nunavut'),
(74, 'CA', 'ON', 'Ontario'),
(75, 'CA', 'PE', 'Prince Edward Island'),
(76, 'CA', 'QC', 'Quebec'),
(77, 'CA', 'SK', 'Saskatchewan'),
(78, 'CA', 'YT', 'Yukon Territory'),
(79, 'DE', 'NDS', 'Niedersachsen'),
(80, 'DE', 'BAW', 'Baden-Württemberg'),
(81, 'DE', 'BAY', 'Bayern'),
(82, 'DE', 'BER', 'Berlin'),
(83, 'DE', 'BRG', 'Brandenburg'),
(84, 'DE', 'BRE', 'Bremen'),
(85, 'DE', 'HAM', 'Hamburg'),
(86, 'DE', 'HES', 'Hessen'),
(87, 'DE', 'MEC', 'Mecklenburg-Vorpommern'),
(88, 'DE', 'NRW', 'Nordrhein-Westfalen'),
(89, 'DE', 'RHE', 'Rheinland-Pfalz'),
(90, 'DE', 'SAR', 'Saarland'),
(91, 'DE', 'SAS', 'Sachsen'),
(92, 'DE', 'SAC', 'Sachsen-Anhalt'),
(93, 'DE', 'SCN', 'Schleswig-Holstein'),
(94, 'DE', 'THE', 'Thüringen'),
(95, 'AT', 'WI', 'Wien'),
(96, 'AT', 'NO', 'Niederösterreich'),
(97, 'AT', 'OO', 'Oberösterreich'),
(98, 'AT', 'SB', 'Salzburg'),
(99, 'AT', 'KN', 'Kärnten'),
(100, 'AT', 'ST', 'Steiermark'),
(101, 'AT', 'TI', 'Tirol'),
(102, 'AT', 'BL', 'Burgenland'),
(103, 'AT', 'VB', 'Vorarlberg'),
(104, 'CH', 'AG', 'Aargau'),
(105, 'CH', 'AI', 'Appenzell Innerrhoden'),
(106, 'CH', 'AR', 'Appenzell Ausserrhoden'),
(107, 'CH', 'BE', 'Bern'),
(108, 'CH', 'BL', 'Basel-Landschaft'),
(109, 'CH', 'BS', 'Basel-Stadt'),
(110, 'CH', 'FR', 'Freiburg'),
(111, 'CH', 'GE', 'Genf'),
(112, 'CH', 'GL', 'Glarus'),
(113, 'CH', 'GR', 'Graubünden'),
(114, 'CH', 'JU', 'Jura'),
(115, 'CH', 'LU', 'Luzern'),
(116, 'CH', 'NE', 'Neuenburg'),
(117, 'CH', 'NW', 'Nidwalden'),
(118, 'CH', 'OW', 'Obwalden'),
(119, 'CH', 'SG', 'St. Gallen'),
(120, 'CH', 'SH', 'Schaffhausen'),
(121, 'CH', 'SO', 'Solothurn'),
(122, 'CH', 'SZ', 'Schwyz'),
(123, 'CH', 'TG', 'Thurgau'),
(124, 'CH', 'TI', 'Tessin'),
(125, 'CH', 'UR', 'Uri'),
(126, 'CH', 'VD', 'Waadt'),
(127, 'CH', 'VS', 'Wallis'),
(128, 'CH', 'ZG', 'Zug'),
(129, 'CH', 'ZH', 'Zürich'),
(130, 'ES', 'A Coruсa', 'A Coruña'),
(131, 'ES', 'Alava', 'Alava'),
(132, 'ES', 'Albacete', 'Albacete'),
(133, 'ES', 'Alicante', 'Alicante'),
(134, 'ES', 'Almeria', 'Almeria'),
(135, 'ES', 'Asturias', 'Asturias'),
(136, 'ES', 'Avila', 'Avila'),
(137, 'ES', 'Badajoz', 'Badajoz'),
(138, 'ES', 'Baleares', 'Baleares'),
(139, 'ES', 'Barcelona', 'Barcelona'),
(140, 'ES', 'Burgos', 'Burgos'),
(141, 'ES', 'Caceres', 'Caceres'),
(142, 'ES', 'Cadiz', 'Cadiz'),
(143, 'ES', 'Cantabria', 'Cantabria'),
(144, 'ES', 'Castellon', 'Castellon'),
(145, 'ES', 'Ceuta', 'Ceuta'),
(146, 'ES', 'Ciudad Real', 'Ciudad Real'),
(147, 'ES', 'Cordoba', 'Cordoba'),
(148, 'ES', 'Cuenca', 'Cuenca'),
(149, 'ES', 'Girona', 'Girona'),
(150, 'ES', 'Granada', 'Granada'),
(151, 'ES', 'Guadalajara', 'Guadalajara'),
(152, 'ES', 'Guipuzcoa', 'Guipuzcoa'),
(153, 'ES', 'Huelva', 'Huelva'),
(154, 'ES', 'Huesca', 'Huesca'),
(155, 'ES', 'Jaen', 'Jaen'),
(156, 'ES', 'La Rioja', 'La Rioja'),
(157, 'ES', 'Las Palmas', 'Las Palmas'),
(158, 'ES', 'Leon', 'Leon'),
(159, 'ES', 'Lleida', 'Lleida'),
(160, 'ES', 'Lugo', 'Lugo'),
(161, 'ES', 'Madrid', 'Madrid'),
(162, 'ES', 'Malaga', 'Malaga'),
(163, 'ES', 'Melilla', 'Melilla'),
(164, 'ES', 'Murcia', 'Murcia'),
(165, 'ES', 'Navarra', 'Navarra'),
(166, 'ES', 'Ourense', 'Ourense'),
(167, 'ES', 'Palencia', 'Palencia'),
(168, 'ES', 'Pontevedra', 'Pontevedra'),
(169, 'ES', 'Salamanca', 'Salamanca'),
(170, 'ES', 'Santa Cruz de Tenerife', 'Santa Cruz de Tenerife'),
(171, 'ES', 'Segovia', 'Segovia'),
(172, 'ES', 'Sevilla', 'Sevilla'),
(173, 'ES', 'Soria', 'Soria'),
(174, 'ES', 'Tarragona', 'Tarragona'),
(175, 'ES', 'Teruel', 'Teruel'),
(176, 'ES', 'Toledo', 'Toledo'),
(177, 'ES', 'Valencia', 'Valencia'),
(178, 'ES', 'Valladolid', 'Valladolid'),
(179, 'ES', 'Vizcaya', 'Vizcaya'),
(180, 'ES', 'Zamora', 'Zamora'),
(181, 'ES', 'Zaragoza', 'Zaragoza'),
(182, 'FR', '1', 'Ain'),
(183, 'FR', '2', 'Aisne'),
(184, 'FR', '3', 'Allier'),
(185, 'FR', '4', 'Alpes-de-Haute-Provence'),
(186, 'FR', '5', 'Hautes-Alpes'),
(187, 'FR', '6', 'Alpes-Maritimes'),
(188, 'FR', '7', 'Ardèche'),
(189, 'FR', '8', 'Ardennes'),
(190, 'FR', '9', 'Ariège'),
(191, 'FR', '10', 'Aube'),
(192, 'FR', '11', 'Aude'),
(193, 'FR', '12', 'Aveyron'),
(194, 'FR', '13', 'Bouches-du-Rhône'),
(195, 'FR', '14', 'Calvados'),
(196, 'FR', '15', 'Cantal'),
(197, 'FR', '16', 'Charente'),
(198, 'FR', '17', 'Charente-Maritime'),
(199, 'FR', '18', 'Cher'),
(200, 'FR', '19', 'Corrèze'),
(201, 'FR', '2A', 'Corse-du-Sud'),
(202, 'FR', '2B', 'Haute-Corse'),
(203, 'FR', '21', 'Côte-d''Or'),
(204, 'FR', '22', 'Côtes-d''Armor'),
(205, 'FR', '23', 'Creuse'),
(206, 'FR', '24', 'Dordogne'),
(207, 'FR', '25', 'Doubs'),
(208, 'FR', '26', 'Drôme'),
(209, 'FR', '27', 'Eure'),
(210, 'FR', '28', 'Eure-et-Loir'),
(211, 'FR', '29', 'Finistère'),
(212, 'FR', '30', 'Gard'),
(213, 'FR', '31', 'Haute-Garonne'),
(214, 'FR', '32', 'Gers'),
(215, 'FR', '33', 'Gironde'),
(216, 'FR', '34', 'Hérault'),
(217, 'FR', '35', 'Ille-et-Vilaine'),
(218, 'FR', '36', 'Indre'),
(219, 'FR', '37', 'Indre-et-Loire'),
(220, 'FR', '38', 'Isère'),
(221, 'FR', '39', 'Jura'),
(222, 'FR', '40', 'Landes'),
(223, 'FR', '41', 'Loir-et-Cher'),
(224, 'FR', '42', 'Loire'),
(225, 'FR', '43', 'Haute-Loire'),
(226, 'FR', '44', 'Loire-Atlantique'),
(227, 'FR', '45', 'Loiret'),
(228, 'FR', '46', 'Lot'),
(229, 'FR', '47', 'Lot-et-Garonne'),
(230, 'FR', '48', 'Lozère'),
(231, 'FR', '49', 'Maine-et-Loire'),
(232, 'FR', '50', 'Manche'),
(233, 'FR', '51', 'Marne'),
(234, 'FR', '52', 'Haute-Marne'),
(235, 'FR', '53', 'Mayenne'),
(236, 'FR', '54', 'Meurthe-et-Moselle'),
(237, 'FR', '55', 'Meuse'),
(238, 'FR', '56', 'Morbihan'),
(239, 'FR', '57', 'Moselle'),
(240, 'FR', '58', 'Nièvre'),
(241, 'FR', '59', 'Nord'),
(242, 'FR', '60', 'Oise'),
(243, 'FR', '61', 'Orne'),
(244, 'FR', '62', 'Pas-de-Calais'),
(245, 'FR', '63', 'Puy-de-Dôme'),
(246, 'FR', '64', 'Pyrénées-Atlantiques'),
(247, 'FR', '65', 'Hautes-Pyrénées'),
(248, 'FR', '66', 'Pyrénées-Orientales'),
(249, 'FR', '67', 'Bas-Rhin'),
(250, 'FR', '68', 'Haut-Rhin'),
(251, 'FR', '69', 'Rhône'),
(252, 'FR', '70', 'Haute-Saône'),
(253, 'FR', '71', 'Saône-et-Loire'),
(254, 'FR', '72', 'Sarthe'),
(255, 'FR', '73', 'Savoie'),
(256, 'FR', '74', 'Haute-Savoie'),
(257, 'FR', '75', 'Paris'),
(258, 'FR', '76', 'Seine-Maritime'),
(259, 'FR', '77', 'Seine-et-Marne'),
(260, 'FR', '78', 'Yvelines'),
(261, 'FR', '79', 'Deux-Sèvres'),
(262, 'FR', '80', 'Somme'),
(263, 'FR', '81', 'Tarn'),
(264, 'FR', '82', 'Tarn-et-Garonne'),
(265, 'FR', '83', 'Var'),
(266, 'FR', '84', 'Vaucluse'),
(267, 'FR', '85', 'Vendée'),
(268, 'FR', '86', 'Vienne'),
(269, 'FR', '87', 'Haute-Vienne'),
(270, 'FR', '88', 'Vosges'),
(271, 'FR', '89', 'Yonne'),
(272, 'FR', '90', 'Territoire-de-Belfort'),
(273, 'FR', '91', 'Essonne'),
(274, 'FR', '92', 'Hauts-de-Seine'),
(275, 'FR', '93', 'Seine-Saint-Denis'),
(276, 'FR', '94', 'Val-de-Marne'),
(277, 'FR', '95', 'Val-d''Oise'),
(278, 'RO', 'AB', 'Alba'),
(279, 'RO', 'AR', 'Arad'),
(280, 'RO', 'AG', 'Argeş'),
(281, 'RO', 'BC', 'Bacău'),
(282, 'RO', 'BH', 'Bihor'),
(283, 'RO', 'BN', 'Bistriţa-Năsăud'),
(284, 'RO', 'BT', 'Botoşani'),
(285, 'RO', 'BV', 'Braşov'),
(286, 'RO', 'BR', 'Brăila'),
(287, 'RO', 'B', 'Bucureşti'),
(288, 'RO', 'BZ', 'Buzău'),
(289, 'RO', 'CS', 'Caraş-Severin'),
(290, 'RO', 'CL', 'Călăraşi'),
(291, 'RO', 'CJ', 'Cluj'),
(292, 'RO', 'CT', 'Constanţa'),
(293, 'RO', 'CV', 'Covasna'),
(294, 'RO', 'DB', 'Dâmboviţa'),
(295, 'RO', 'DJ', 'Dolj'),
(296, 'RO', 'GL', 'Galaţi'),
(297, 'RO', 'GR', 'Giurgiu'),
(298, 'RO', 'GJ', 'Gorj'),
(299, 'RO', 'HR', 'Harghita'),
(300, 'RO', 'HD', 'Hunedoara'),
(301, 'RO', 'IL', 'Ialomiţa'),
(302, 'RO', 'IS', 'Iaşi'),
(303, 'RO', 'IF', 'Ilfov'),
(304, 'RO', 'MM', 'Maramureş'),
(305, 'RO', 'MH', 'Mehedinţi'),
(306, 'RO', 'MS', 'Mureş'),
(307, 'RO', 'NT', 'Neamţ'),
(308, 'RO', 'OT', 'Olt'),
(309, 'RO', 'PH', 'Prahova'),
(310, 'RO', 'SM', 'Satu-Mare'),
(311, 'RO', 'SJ', 'Sălaj'),
(312, 'RO', 'SB', 'Sibiu'),
(313, 'RO', 'SV', 'Suceava'),
(314, 'RO', 'TR', 'Teleorman'),
(315, 'RO', 'TM', 'Timiş'),
(316, 'RO', 'TL', 'Tulcea'),
(317, 'RO', 'VS', 'Vaslui'),
(318, 'RO', 'VL', 'Vâlcea'),
(319, 'RO', 'VN', 'Vrancea'),
(320, 'FI', 'Lappi', 'Lappi'),
(321, 'FI', 'Pohjois-Pohjanmaa', 'Pohjois-Pohjanmaa'),
(322, 'FI', 'Kainuu', 'Kainuu'),
(323, 'FI', 'Pohjois-Karjala', 'Pohjois-Karjala'),
(324, 'FI', 'Pohjois-Savo', 'Pohjois-Savo'),
(325, 'FI', 'Etelä-Savo', 'Etelä-Savo'),
(326, 'FI', 'Etelä-Pohjanmaa', 'Etelä-Pohjanmaa'),
(327, 'FI', 'Pohjanmaa', 'Pohjanmaa'),
(328, 'FI', 'Pirkanmaa', 'Pirkanmaa'),
(329, 'FI', 'Satakunta', 'Satakunta'),
(330, 'FI', 'Keski-Pohjanmaa', 'Keski-Pohjanmaa'),
(331, 'FI', 'Keski-Suomi', 'Keski-Suomi'),
(332, 'FI', 'Varsinais-Suomi', 'Varsinais-Suomi'),
(333, 'FI', 'Etelä-Karjala', 'Etelä-Karjala'),
(334, 'FI', 'Päijät-Häme', 'Päijät-Häme'),
(335, 'FI', 'Kanta-Häme', 'Kanta-Häme'),
(336, 'FI', 'Uusimaa', 'Uusimaa'),
(337, 'FI', 'Itä-Uusimaa', 'Itä-Uusimaa'),
(338, 'FI', 'Kymenlaakso', 'Kymenlaakso'),
(339, 'FI', 'Ahvenanmaa', 'Ahvenanmaa'),
(340, 'EE', 'EE-37', 'Harjumaa'),
(341, 'EE', 'EE-39', 'Hiiumaa'),
(342, 'EE', 'EE-44', 'Ida-Virumaa'),
(343, 'EE', 'EE-49', 'Jõgevamaa'),
(344, 'EE', 'EE-51', 'Järvamaa'),
(345, 'EE', 'EE-57', 'Läänemaa'),
(346, 'EE', 'EE-59', 'Lääne-Virumaa'),
(347, 'EE', 'EE-65', 'Põlvamaa'),
(348, 'EE', 'EE-67', 'Pärnumaa'),
(349, 'EE', 'EE-70', 'Raplamaa'),
(350, 'EE', 'EE-74', 'Saaremaa'),
(351, 'EE', 'EE-78', 'Tartumaa'),
(352, 'EE', 'EE-82', 'Valgamaa'),
(353, 'EE', 'EE-84', 'Viljandimaa'),
(354, 'EE', 'EE-86', 'Võrumaa'),
(355, 'LV', 'LV-DGV', 'Daugavpils'),
(356, 'LV', 'LV-JEL', 'Jelgava'),
(357, 'LV', 'Jēkabpils', 'Jēkabpils'),
(358, 'LV', 'LV-JUR', 'Jūrmala'),
(359, 'LV', 'LV-LPX', 'Liepāja'),
(360, 'LV', 'LV-LE', 'Liepājas novads'),
(361, 'LV', 'LV-REZ', 'Rēzekne'),
(362, 'LV', 'LV-RIX', 'Rīga'),
(363, 'LV', 'LV-RI', 'Rīgas novads'),
(364, 'LV', 'Valmiera', 'Valmiera'),
(365, 'LV', 'LV-VEN', 'Ventspils'),
(366, 'LV', 'Aglonas novads', 'Aglonas novads'),
(367, 'LV', 'LV-AI', 'Aizkraukles novads'),
(368, 'LV', 'Aizputes novads', 'Aizputes novads'),
(369, 'LV', 'Aknīstes novads', 'Aknīstes novads'),
(370, 'LV', 'Alojas novads', 'Alojas novads'),
(371, 'LV', 'Alsungas novads', 'Alsungas novads'),
(372, 'LV', 'LV-AL', 'Alūksnes novads'),
(373, 'LV', 'Amatas novads', 'Amatas novads'),
(374, 'LV', 'Apes novads', 'Apes novads'),
(375, 'LV', 'Auces novads', 'Auces novads'),
(376, 'LV', 'Babītes novads', 'Babītes novads'),
(377, 'LV', 'Baldones novads', 'Baldones novads'),
(378, 'LV', 'Baltinavas novads', 'Baltinavas novads'),
(379, 'LV', 'LV-BL', 'Balvu novads'),
(380, 'LV', 'LV-BU', 'Bauskas novads'),
(381, 'LV', 'Beverīnas novads', 'Beverīnas novads'),
(382, 'LV', 'Brocēnu novads', 'Brocēnu novads'),
(383, 'LV', 'Burtnieku novads', 'Burtnieku novads'),
(384, 'LV', 'Carnikavas novads', 'Carnikavas novads'),
(385, 'LV', 'Cesvaines novads', 'Cesvaines novads'),
(386, 'LV', 'Ciblas novads', 'Ciblas novads'),
(387, 'LV', 'LV-CE', 'Cēsu novads'),
(388, 'LV', 'Dagdas novads', 'Dagdas novads'),
(389, 'LV', 'LV-DA', 'Daugavpils novads'),
(390, 'LV', 'LV-DO', 'Dobeles novads'),
(391, 'LV', 'Dundagas novads', 'Dundagas novads'),
(392, 'LV', 'Durbes novads', 'Durbes novads'),
(393, 'LV', 'Engures novads', 'Engures novads'),
(394, 'LV', 'Garkalnes novads', 'Garkalnes novads'),
(395, 'LV', 'Grobiņas novads', 'Grobiņas novads'),
(396, 'LV', 'LV-GU', 'Gulbenes novads'),
(397, 'LV', 'Iecavas novads', 'Iecavas novads'),
(398, 'LV', 'Ikšķiles novads', 'Ikšķiles novads'),
(399, 'LV', 'Ilūkstes novads', 'Ilūkstes novads'),
(400, 'LV', 'Inčukalna novads', 'Inčukalna novads'),
(401, 'LV', 'Jaunjelgavas novads', 'Jaunjelgavas novads'),
(402, 'LV', 'Jaunpiebalgas novads', 'Jaunpiebalgas novads'),
(403, 'LV', 'Jaunpils novads', 'Jaunpils novads'),
(404, 'LV', 'LV-JL', 'Jelgavas novads'),
(405, 'LV', 'LV-JK', 'Jēkabpils novads'),
(406, 'LV', 'Kandavas novads', 'Kandavas novads'),
(407, 'LV', 'Kokneses novads', 'Kokneses novads'),
(408, 'LV', 'Krimuldas novads', 'Krimuldas novads'),
(409, 'LV', 'Krustpils novads', 'Krustpils novads'),
(410, 'LV', 'LV-KR', 'Krāslavas novads'),
(411, 'LV', 'LV-KU', 'Kuldīgas novads'),
(412, 'LV', 'Kārsavas novads', 'Kārsavas novads'),
(413, 'LV', 'Lielvārdes novads', 'Lielvārdes novads'),
(414, 'LV', 'LV-LM', 'Limbažu novads'),
(415, 'LV', 'Lubānas novads', 'Lubānas novads'),
(416, 'LV', 'LV-LU', 'Ludzas novads'),
(417, 'LV', 'Līgatnes novads', 'Līgatnes novads'),
(418, 'LV', 'Līvānu novads', 'Līvānu novads'),
(419, 'LV', 'LV-MA', 'Madonas novads'),
(420, 'LV', 'Mazsalacas novads', 'Mazsalacas novads'),
(421, 'LV', 'Mālpils novads', 'Mālpils novads'),
(422, 'LV', 'Mārupes novads', 'Mārupes novads'),
(423, 'LV', 'Naukšēnu novads', 'Naukšēnu novads'),
(424, 'LV', 'Neretas novads', 'Neretas novads'),
(425, 'LV', 'Nīcas novads', 'Nīcas novads'),
(426, 'LV', 'LV-OG', 'Ogres novads'),
(427, 'LV', 'Olaines novads', 'Olaines novads'),
(428, 'LV', 'Ozolnieku novads', 'Ozolnieku novads'),
(429, 'LV', 'LV-PR', 'Preiļu novads'),
(430, 'LV', 'Priekules novads', 'Priekules novads'),
(431, 'LV', 'Priekuļu novads', 'Priekuļu novads'),
(432, 'LV', 'Pārgaujas novads', 'Pārgaujas novads'),
(433, 'LV', 'Pāvilostas novads', 'Pāvilostas novads'),
(434, 'LV', 'Pļaviņu novads', 'Pļaviņu novads'),
(435, 'LV', 'Raunas novads', 'Raunas novads'),
(436, 'LV', 'Riebiņu novads', 'Riebiņu novads'),
(437, 'LV', 'Rojas novads', 'Rojas novads'),
(438, 'LV', 'Ropažu novads', 'Ropažu novads'),
(439, 'LV', 'Rucavas novads', 'Rucavas novads'),
(440, 'LV', 'Rugāju novads', 'Rugāju novads'),
(441, 'LV', 'Rundāles novads', 'Rundāles novads'),
(442, 'LV', 'LV-RE', 'Rēzeknes novads'),
(443, 'LV', 'Rūjienas novads', 'Rūjienas novads'),
(444, 'LV', 'Salacgrīvas novads', 'Salacgrīvas novads'),
(445, 'LV', 'Salas novads', 'Salas novads'),
(446, 'LV', 'Salaspils novads', 'Salaspils novads'),
(447, 'LV', 'LV-SA', 'Saldus novads'),
(448, 'LV', 'Saulkrastu novads', 'Saulkrastu novads'),
(449, 'LV', 'Siguldas novads', 'Siguldas novads'),
(450, 'LV', 'Skrundas novads', 'Skrundas novads'),
(451, 'LV', 'Skrīveru novads', 'Skrīveru novads'),
(452, 'LV', 'Smiltenes novads', 'Smiltenes novads'),
(453, 'LV', 'Stopiņu novads', 'Stopiņu novads'),
(454, 'LV', 'Strenču novads', 'Strenču novads'),
(455, 'LV', 'Sējas novads', 'Sējas novads'),
(456, 'LV', 'LV-TA', 'Talsu novads'),
(457, 'LV', 'LV-TU', 'Tukuma novads'),
(458, 'LV', 'Tērvetes novads', 'Tērvetes novads'),
(459, 'LV', 'Vaiņodes novads', 'Vaiņodes novads'),
(460, 'LV', 'LV-VK', 'Valkas novads'),
(461, 'LV', 'LV-VM', 'Valmieras novads'),
(462, 'LV', 'Varakļānu novads', 'Varakļānu novads'),
(463, 'LV', 'Vecpiebalgas novads', 'Vecpiebalgas novads'),
(464, 'LV', 'Vecumnieku novads', 'Vecumnieku novads'),
(465, 'LV', 'LV-VE', 'Ventspils novads'),
(466, 'LV', 'Viesītes novads', 'Viesītes novads'),
(467, 'LV', 'Viļakas novads', 'Viļakas novads'),
(468, 'LV', 'Viļānu novads', 'Viļānu novads'),
(469, 'LV', 'Vārkavas novads', 'Vārkavas novads'),
(470, 'LV', 'Zilupes novads', 'Zilupes novads'),
(471, 'LV', 'Ādažu novads', 'Ādažu novads'),
(472, 'LV', 'Ērgļu novads', 'Ērgļu novads'),
(473, 'LV', 'Ķeguma novads', 'Ķeguma novads'),
(474, 'LV', 'Ķekavas novads', 'Ķekavas novads'),
(475, 'LT', 'LT-AL', 'Alytaus Apskritis'),
(476, 'LT', 'LT-KU', 'Kauno Apskritis'),
(477, 'LT', 'LT-KL', 'Klaipėdos Apskritis'),
(478, 'LT', 'LT-MR', 'Marijampolės Apskritis'),
(479, 'LT', 'LT-PN', 'Panevėžio Apskritis'),
(480, 'LT', 'LT-SA', 'Šiaulių Apskritis'),
(481, 'LT', 'LT-TA', 'Tauragės Apskritis'),
(482, 'LT', 'LT-TE', 'Telšių Apskritis'),
(483, 'LT', 'LT-UT', 'Utenos Apskritis'),
(484, 'LT', 'LT-VL', 'Vilniaus Apskritis'),
(485, 'BR', 'AC', 'Acre'),
(486, 'BR', 'AL', 'Alagoas'),
(487, 'BR', 'AP', 'Amapá'),
(488, 'BR', 'AM', 'Amazonas'),
(489, 'BR', 'BA', 'Bahia'),
(490, 'BR', 'CE', 'Ceará'),
(491, 'BR', 'ES', 'Espírito Santo'),
(492, 'BR', 'GO', 'Goiás'),
(493, 'BR', 'MA', 'Maranhão'),
(494, 'BR', 'MT', 'Mato Grosso'),
(495, 'BR', 'MS', 'Mato Grosso do Sul'),
(496, 'BR', 'MG', 'Minas Gerais'),
(497, 'BR', 'PA', 'Pará'),
(498, 'BR', 'PB', 'Paraíba'),
(499, 'BR', 'PR', 'Paraná'),
(500, 'BR', 'PE', 'Pernambuco'),
(501, 'BR', 'PI', 'Piauí'),
(502, 'BR', 'RJ', 'Rio de Janeiro'),
(503, 'BR', 'RN', 'Rio Grande do Norte'),
(504, 'BR', 'RS', 'Rio Grande do Sul'),
(505, 'BR', 'RO', 'Rondônia'),
(506, 'BR', 'RR', 'Roraima'),
(507, 'BR', 'SC', 'Santa Catarina'),
(508, 'BR', 'SP', 'São Paulo'),
(509, 'BR', 'SE', 'Sergipe'),
(510, 'BR', 'TO', 'Tocantins'),
(511, 'BR', 'DF', 'Distrito Federal');

-- --------------------------------------------------------

--
-- Table structure for table `directory_country_region_name`
--

CREATE TABLE `directory_country_region_name` (
  `locale` varchar(8) NOT NULL COMMENT 'Locale',
  `region_id` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Region Id',
  `name` varchar(255) DEFAULT NULL COMMENT 'Region Name'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Directory Country Region Name';

--
-- Dumping data for table `directory_country_region_name`
--

INSERT INTO `directory_country_region_name` (`locale`, `region_id`, `name`) VALUES
('en_US', 1, 'Alabama'),
('en_US', 2, 'Alaska'),
('en_US', 3, 'American Samoa'),
('en_US', 4, 'Arizona'),
('en_US', 5, 'Arkansas'),
('en_US', 6, 'Armed Forces Africa'),
('en_US', 7, 'Armed Forces Americas'),
('en_US', 8, 'Armed Forces Canada'),
('en_US', 9, 'Armed Forces Europe'),
('en_US', 10, 'Armed Forces Middle East'),
('en_US', 11, 'Armed Forces Pacific'),
('en_US', 12, 'California'),
('en_US', 13, 'Colorado'),
('en_US', 14, 'Connecticut'),
('en_US', 15, 'Delaware'),
('en_US', 16, 'District of Columbia'),
('en_US', 17, 'Federated States Of Micronesia'),
('en_US', 18, 'Florida'),
('en_US', 19, 'Georgia'),
('en_US', 20, 'Guam'),
('en_US', 21, 'Hawaii'),
('en_US', 22, 'Idaho'),
('en_US', 23, 'Illinois'),
('en_US', 24, 'Indiana'),
('en_US', 25, 'Iowa'),
('en_US', 26, 'Kansas'),
('en_US', 27, 'Kentucky'),
('en_US', 28, 'Louisiana'),
('en_US', 29, 'Maine'),
('en_US', 30, 'Marshall Islands'),
('en_US', 31, 'Maryland'),
('en_US', 32, 'Massachusetts'),
('en_US', 33, 'Michigan'),
('en_US', 34, 'Minnesota'),
('en_US', 35, 'Mississippi'),
('en_US', 36, 'Missouri'),
('en_US', 37, 'Montana'),
('en_US', 38, 'Nebraska'),
('en_US', 39, 'Nevada'),
('en_US', 40, 'New Hampshire'),
('en_US', 41, 'New Jersey'),
('en_US', 42, 'New Mexico'),
('en_US', 43, 'New York'),
('en_US', 44, 'North Carolina'),
('en_US', 45, 'North Dakota'),
('en_US', 46, 'Northern Mariana Islands'),
('en_US', 47, 'Ohio'),
('en_US', 48, 'Oklahoma'),
('en_US', 49, 'Oregon'),
('en_US', 50, 'Palau'),
('en_US', 51, 'Pennsylvania'),
('en_US', 52, 'Puerto Rico'),
('en_US', 53, 'Rhode Island'),
('en_US', 54, 'South Carolina'),
('en_US', 55, 'South Dakota'),
('en_US', 56, 'Tennessee'),
('en_US', 57, 'Texas'),
('en_US', 58, 'Utah'),
('en_US', 59, 'Vermont'),
('en_US', 60, 'Virgin Islands'),
('en_US', 61, 'Virginia'),
('en_US', 62, 'Washington'),
('en_US', 63, 'West Virginia'),
('en_US', 64, 'Wisconsin'),
('en_US', 65, 'Wyoming'),
('en_US', 66, 'Alberta'),
('en_US', 67, 'British Columbia'),
('en_US', 68, 'Manitoba'),
('en_US', 69, 'Newfoundland and Labrador'),
('en_US', 70, 'New Brunswick'),
('en_US', 71, 'Nova Scotia'),
('en_US', 72, 'Northwest Territories'),
('en_US', 73, 'Nunavut'),
('en_US', 74, 'Ontario'),
('en_US', 75, 'Prince Edward Island'),
('en_US', 76, 'Quebec'),
('en_US', 77, 'Saskatchewan'),
('en_US', 78, 'Yukon Territory'),
('en_US', 79, 'Niedersachsen'),
('en_US', 80, 'Baden-Württemberg'),
('en_US', 81, 'Bayern'),
('en_US', 82, 'Berlin'),
('en_US', 83, 'Brandenburg'),
('en_US', 84, 'Bremen'),
('en_US', 85, 'Hamburg'),
('en_US', 86, 'Hessen'),
('en_US', 87, 'Mecklenburg-Vorpommern'),
('en_US', 88, 'Nordrhein-Westfalen'),
('en_US', 89, 'Rheinland-Pfalz'),
('en_US', 90, 'Saarland'),
('en_US', 91, 'Sachsen'),
('en_US', 92, 'Sachsen-Anhalt'),
('en_US', 93, 'Schleswig-Holstein'),
('en_US', 94, 'Thüringen'),
('en_US', 95, 'Wien'),
('en_US', 96, 'Niederösterreich'),
('en_US', 97, 'Oberösterreich'),
('en_US', 98, 'Salzburg'),
('en_US', 99, 'Kärnten'),
('en_US', 100, 'Steiermark'),
('en_US', 101, 'Tirol'),
('en_US', 102, 'Burgenland'),
('en_US', 103, 'Vorarlberg'),
('en_US', 104, 'Aargau'),
('en_US', 105, 'Appenzell Innerrhoden'),
('en_US', 106, 'Appenzell Ausserrhoden'),
('en_US', 107, 'Bern'),
('en_US', 108, 'Basel-Landschaft'),
('en_US', 109, 'Basel-Stadt'),
('en_US', 110, 'Freiburg'),
('en_US', 111, 'Genf'),
('en_US', 112, 'Glarus'),
('en_US', 113, 'Graubünden'),
('en_US', 114, 'Jura'),
('en_US', 115, 'Luzern'),
('en_US', 116, 'Neuenburg'),
('en_US', 117, 'Nidwalden'),
('en_US', 118, 'Obwalden'),
('en_US', 119, 'St. Gallen'),
('en_US', 120, 'Schaffhausen'),
('en_US', 121, 'Solothurn'),
('en_US', 122, 'Schwyz'),
('en_US', 123, 'Thurgau'),
('en_US', 124, 'Tessin'),
('en_US', 125, 'Uri'),
('en_US', 126, 'Waadt'),
('en_US', 127, 'Wallis'),
('en_US', 128, 'Zug'),
('en_US', 129, 'Zürich'),
('en_US', 130, 'A Coruña'),
('en_US', 131, 'Alava'),
('en_US', 132, 'Albacete'),
('en_US', 133, 'Alicante'),
('en_US', 134, 'Almeria'),
('en_US', 135, 'Asturias'),
('en_US', 136, 'Avila'),
('en_US', 137, 'Badajoz'),
('en_US', 138, 'Baleares'),
('en_US', 139, 'Barcelona'),
('en_US', 140, 'Burgos'),
('en_US', 141, 'Caceres'),
('en_US', 142, 'Cadiz'),
('en_US', 143, 'Cantabria'),
('en_US', 144, 'Castellon'),
('en_US', 145, 'Ceuta'),
('en_US', 146, 'Ciudad Real'),
('en_US', 147, 'Cordoba'),
('en_US', 148, 'Cuenca'),
('en_US', 149, 'Girona'),
('en_US', 150, 'Granada'),
('en_US', 151, 'Guadalajara'),
('en_US', 152, 'Guipuzcoa'),
('en_US', 153, 'Huelva'),
('en_US', 154, 'Huesca'),
('en_US', 155, 'Jaen'),
('en_US', 156, 'La Rioja'),
('en_US', 157, 'Las Palmas'),
('en_US', 158, 'Leon'),
('en_US', 159, 'Lleida'),
('en_US', 160, 'Lugo'),
('en_US', 161, 'Madrid'),
('en_US', 162, 'Malaga'),
('en_US', 163, 'Melilla'),
('en_US', 164, 'Murcia'),
('en_US', 165, 'Navarra'),
('en_US', 166, 'Ourense'),
('en_US', 167, 'Palencia'),
('en_US', 168, 'Pontevedra'),
('en_US', 169, 'Salamanca'),
('en_US', 170, 'Santa Cruz de Tenerife'),
('en_US', 171, 'Segovia'),
('en_US', 172, 'Sevilla'),
('en_US', 173, 'Soria'),
('en_US', 174, 'Tarragona'),
('en_US', 175, 'Teruel'),
('en_US', 176, 'Toledo'),
('en_US', 177, 'Valencia'),
('en_US', 178, 'Valladolid'),
('en_US', 179, 'Vizcaya'),
('en_US', 180, 'Zamora'),
('en_US', 181, 'Zaragoza'),
('en_US', 182, 'Ain'),
('en_US', 183, 'Aisne'),
('en_US', 184, 'Allier'),
('en_US', 185, 'Alpes-de-Haute-Provence'),
('en_US', 186, 'Hautes-Alpes'),
('en_US', 187, 'Alpes-Maritimes'),
('en_US', 188, 'Ardèche'),
('en_US', 189, 'Ardennes'),
('en_US', 190, 'Ariège'),
('en_US', 191, 'Aube'),
('en_US', 192, 'Aude'),
('en_US', 193, 'Aveyron'),
('en_US', 194, 'Bouches-du-Rhône'),
('en_US', 195, 'Calvados'),
('en_US', 196, 'Cantal'),
('en_US', 197, 'Charente'),
('en_US', 198, 'Charente-Maritime'),
('en_US', 199, 'Cher'),
('en_US', 200, 'Corrèze'),
('en_US', 201, 'Corse-du-Sud'),
('en_US', 202, 'Haute-Corse'),
('en_US', 203, 'Côte-d''Or'),
('en_US', 204, 'Côtes-d''Armor'),
('en_US', 205, 'Creuse'),
('en_US', 206, 'Dordogne'),
('en_US', 207, 'Doubs'),
('en_US', 208, 'Drôme'),
('en_US', 209, 'Eure'),
('en_US', 210, 'Eure-et-Loir'),
('en_US', 211, 'Finistère'),
('en_US', 212, 'Gard'),
('en_US', 213, 'Haute-Garonne'),
('en_US', 214, 'Gers'),
('en_US', 215, 'Gironde'),
('en_US', 216, 'Hérault'),
('en_US', 217, 'Ille-et-Vilaine'),
('en_US', 218, 'Indre'),
('en_US', 219, 'Indre-et-Loire'),
('en_US', 220, 'Isère'),
('en_US', 221, 'Jura'),
('en_US', 222, 'Landes'),
('en_US', 223, 'Loir-et-Cher'),
('en_US', 224, 'Loire'),
('en_US', 225, 'Haute-Loire'),
('en_US', 226, 'Loire-Atlantique'),
('en_US', 227, 'Loiret'),
('en_US', 228, 'Lot'),
('en_US', 229, 'Lot-et-Garonne'),
('en_US', 230, 'Lozère'),
('en_US', 231, 'Maine-et-Loire'),
('en_US', 232, 'Manche'),
('en_US', 233, 'Marne'),
('en_US', 234, 'Haute-Marne'),
('en_US', 235, 'Mayenne'),
('en_US', 236, 'Meurthe-et-Moselle'),
('en_US', 237, 'Meuse'),
('en_US', 238, 'Morbihan'),
('en_US', 239, 'Moselle'),
('en_US', 240, 'Nièvre'),
('en_US', 241, 'Nord'),
('en_US', 242, 'Oise'),
('en_US', 243, 'Orne'),
('en_US', 244, 'Pas-de-Calais'),
('en_US', 245, 'Puy-de-Dôme'),
('en_US', 246, 'Pyrénées-Atlantiques'),
('en_US', 247, 'Hautes-Pyrénées'),
('en_US', 248, 'Pyrénées-Orientales'),
('en_US', 249, 'Bas-Rhin'),
('en_US', 250, 'Haut-Rhin'),
('en_US', 251, 'Rhône'),
('en_US', 252, 'Haute-Saône'),
('en_US', 253, 'Saône-et-Loire'),
('en_US', 254, 'Sarthe'),
('en_US', 255, 'Savoie'),
('en_US', 256, 'Haute-Savoie'),
('en_US', 257, 'Paris'),
('en_US', 258, 'Seine-Maritime'),
('en_US', 259, 'Seine-et-Marne'),
('en_US', 260, 'Yvelines'),
('en_US', 261, 'Deux-Sèvres'),
('en_US', 262, 'Somme'),
('en_US', 263, 'Tarn'),
('en_US', 264, 'Tarn-et-Garonne'),
('en_US', 265, 'Var'),
('en_US', 266, 'Vaucluse'),
('en_US', 267, 'Vendée'),
('en_US', 268, 'Vienne'),
('en_US', 269, 'Haute-Vienne'),
('en_US', 270, 'Vosges'),
('en_US', 271, 'Yonne'),
('en_US', 272, 'Territoire-de-Belfort'),
('en_US', 273, 'Essonne'),
('en_US', 274, 'Hauts-de-Seine'),
('en_US', 275, 'Seine-Saint-Denis'),
('en_US', 276, 'Val-de-Marne'),
('en_US', 277, 'Val-d''Oise'),
('en_US', 278, 'Alba'),
('en_US', 279, 'Arad'),
('en_US', 280, 'Argeş'),
('en_US', 281, 'Bacău'),
('en_US', 282, 'Bihor'),
('en_US', 283, 'Bistriţa-Năsăud'),
('en_US', 284, 'Botoşani'),
('en_US', 285, 'Braşov'),
('en_US', 286, 'Brăila'),
('en_US', 287, 'Bucureşti'),
('en_US', 288, 'Buzău'),
('en_US', 289, 'Caraş-Severin'),
('en_US', 290, 'Călăraşi'),
('en_US', 291, 'Cluj'),
('en_US', 292, 'Constanţa'),
('en_US', 293, 'Covasna'),
('en_US', 294, 'Dâmboviţa'),
('en_US', 295, 'Dolj'),
('en_US', 296, 'Galaţi'),
('en_US', 297, 'Giurgiu'),
('en_US', 298, 'Gorj'),
('en_US', 299, 'Harghita'),
('en_US', 300, 'Hunedoara'),
('en_US', 301, 'Ialomiţa'),
('en_US', 302, 'Iaşi'),
('en_US', 303, 'Ilfov'),
('en_US', 304, 'Maramureş'),
('en_US', 305, 'Mehedinţi'),
('en_US', 306, 'Mureş'),
('en_US', 307, 'Neamţ'),
('en_US', 308, 'Olt'),
('en_US', 309, 'Prahova'),
('en_US', 310, 'Satu-Mare'),
('en_US', 311, 'Sălaj'),
('en_US', 312, 'Sibiu'),
('en_US', 313, 'Suceava'),
('en_US', 314, 'Teleorman'),
('en_US', 315, 'Timiş'),
('en_US', 316, 'Tulcea'),
('en_US', 317, 'Vaslui'),
('en_US', 318, 'Vâlcea'),
('en_US', 319, 'Vrancea'),
('en_US', 320, 'Lappi'),
('en_US', 321, 'Pohjois-Pohjanmaa'),
('en_US', 322, 'Kainuu'),
('en_US', 323, 'Pohjois-Karjala'),
('en_US', 324, 'Pohjois-Savo'),
('en_US', 325, 'Etelä-Savo'),
('en_US', 326, 'Etelä-Pohjanmaa'),
('en_US', 327, 'Pohjanmaa'),
('en_US', 328, 'Pirkanmaa'),
('en_US', 329, 'Satakunta'),
('en_US', 330, 'Keski-Pohjanmaa'),
('en_US', 331, 'Keski-Suomi'),
('en_US', 332, 'Varsinais-Suomi'),
('en_US', 333, 'Etelä-Karjala'),
('en_US', 334, 'Päijät-Häme'),
('en_US', 335, 'Kanta-Häme'),
('en_US', 336, 'Uusimaa'),
('en_US', 337, 'Itä-Uusimaa'),
('en_US', 338, 'Kymenlaakso'),
('en_US', 339, 'Ahvenanmaa'),
('en_US', 340, 'Harjumaa'),
('en_US', 341, 'Hiiumaa'),
('en_US', 342, 'Ida-Virumaa'),
('en_US', 343, 'Jõgevamaa'),
('en_US', 344, 'Järvamaa'),
('en_US', 345, 'Läänemaa'),
('en_US', 346, 'Lääne-Virumaa'),
('en_US', 347, 'Põlvamaa'),
('en_US', 348, 'Pärnumaa'),
('en_US', 349, 'Raplamaa'),
('en_US', 350, 'Saaremaa'),
('en_US', 351, 'Tartumaa'),
('en_US', 352, 'Valgamaa'),
('en_US', 353, 'Viljandimaa'),
('en_US', 354, 'Võrumaa'),
('en_US', 355, 'Daugavpils'),
('en_US', 356, 'Jelgava'),
('en_US', 357, 'Jēkabpils'),
('en_US', 358, 'Jūrmala'),
('en_US', 359, 'Liepāja'),
('en_US', 360, 'Liepājas novads'),
('en_US', 361, 'Rēzekne'),
('en_US', 362, 'Rīga'),
('en_US', 363, 'Rīgas novads'),
('en_US', 364, 'Valmiera'),
('en_US', 365, 'Ventspils'),
('en_US', 366, 'Aglonas novads'),
('en_US', 367, 'Aizkraukles novads'),
('en_US', 368, 'Aizputes novads'),
('en_US', 369, 'Aknīstes novads'),
('en_US', 370, 'Alojas novads'),
('en_US', 371, 'Alsungas novads'),
('en_US', 372, 'Alūksnes novads'),
('en_US', 373, 'Amatas novads'),
('en_US', 374, 'Apes novads'),
('en_US', 375, 'Auces novads'),
('en_US', 376, 'Babītes novads'),
('en_US', 377, 'Baldones novads'),
('en_US', 378, 'Baltinavas novads'),
('en_US', 379, 'Balvu novads'),
('en_US', 380, 'Bauskas novads'),
('en_US', 381, 'Beverīnas novads'),
('en_US', 382, 'Brocēnu novads'),
('en_US', 383, 'Burtnieku novads'),
('en_US', 384, 'Carnikavas novads'),
('en_US', 385, 'Cesvaines novads'),
('en_US', 386, 'Ciblas novads'),
('en_US', 387, 'Cēsu novads'),
('en_US', 388, 'Dagdas novads'),
('en_US', 389, 'Daugavpils novads'),
('en_US', 390, 'Dobeles novads'),
('en_US', 391, 'Dundagas novads'),
('en_US', 392, 'Durbes novads'),
('en_US', 393, 'Engures novads'),
('en_US', 394, 'Garkalnes novads'),
('en_US', 395, 'Grobiņas novads'),
('en_US', 396, 'Gulbenes novads'),
('en_US', 397, 'Iecavas novads'),
('en_US', 398, 'Ikšķiles novads'),
('en_US', 399, 'Ilūkstes novads'),
('en_US', 400, 'Inčukalna novads'),
('en_US', 401, 'Jaunjelgavas novads'),
('en_US', 402, 'Jaunpiebalgas novads'),
('en_US', 403, 'Jaunpils novads'),
('en_US', 404, 'Jelgavas novads'),
('en_US', 405, 'Jēkabpils novads'),
('en_US', 406, 'Kandavas novads'),
('en_US', 407, 'Kokneses novads'),
('en_US', 408, 'Krimuldas novads'),
('en_US', 409, 'Krustpils novads'),
('en_US', 410, 'Krāslavas novads'),
('en_US', 411, 'Kuldīgas novads'),
('en_US', 412, 'Kārsavas novads'),
('en_US', 413, 'Lielvārdes novads'),
('en_US', 414, 'Limbažu novads'),
('en_US', 415, 'Lubānas novads'),
('en_US', 416, 'Ludzas novads'),
('en_US', 417, 'Līgatnes novads'),
('en_US', 418, 'Līvānu novads'),
('en_US', 419, 'Madonas novads'),
('en_US', 420, 'Mazsalacas novads'),
('en_US', 421, 'Mālpils novads'),
('en_US', 422, 'Mārupes novads'),
('en_US', 423, 'Naukšēnu novads'),
('en_US', 424, 'Neretas novads'),
('en_US', 425, 'Nīcas novads'),
('en_US', 426, 'Ogres novads'),
('en_US', 427, 'Olaines novads'),
('en_US', 428, 'Ozolnieku novads'),
('en_US', 429, 'Preiļu novads'),
('en_US', 430, 'Priekules novads'),
('en_US', 431, 'Priekuļu novads'),
('en_US', 432, 'Pārgaujas novads'),
('en_US', 433, 'Pāvilostas novads'),
('en_US', 434, 'Pļaviņu novads'),
('en_US', 435, 'Raunas novads'),
('en_US', 436, 'Riebiņu novads'),
('en_US', 437, 'Rojas novads'),
('en_US', 438, 'Ropažu novads'),
('en_US', 439, 'Rucavas novads'),
('en_US', 440, 'Rugāju novads'),
('en_US', 441, 'Rundāles novads'),
('en_US', 442, 'Rēzeknes novads'),
('en_US', 443, 'Rūjienas novads'),
('en_US', 444, 'Salacgrīvas novads'),
('en_US', 445, 'Salas novads'),
('en_US', 446, 'Salaspils novads'),
('en_US', 447, 'Saldus novads'),
('en_US', 448, 'Saulkrastu novads'),
('en_US', 449, 'Siguldas novads'),
('en_US', 450, 'Skrundas novads'),
('en_US', 451, 'Skrīveru novads'),
('en_US', 452, 'Smiltenes novads'),
('en_US', 453, 'Stopiņu novads'),
('en_US', 454, 'Strenču novads'),
('en_US', 455, 'Sējas novads'),
('en_US', 456, 'Talsu novads'),
('en_US', 457, 'Tukuma novads'),
('en_US', 458, 'Tērvetes novads'),
('en_US', 459, 'Vaiņodes novads'),
('en_US', 460, 'Valkas novads'),
('en_US', 461, 'Valmieras novads'),
('en_US', 462, 'Varakļānu novads'),
('en_US', 463, 'Vecpiebalgas novads'),
('en_US', 464, 'Vecumnieku novads'),
('en_US', 465, 'Ventspils novads'),
('en_US', 466, 'Viesītes novads'),
('en_US', 467, 'Viļakas novads'),
('en_US', 468, 'Viļānu novads'),
('en_US', 469, 'Vārkavas novads'),
('en_US', 470, 'Zilupes novads'),
('en_US', 471, 'Ādažu novads'),
('en_US', 472, 'Ērgļu novads'),
('en_US', 473, 'Ķeguma novads'),
('en_US', 474, 'Ķekavas novads'),
('en_US', 475, 'Alytaus Apskritis'),
('en_US', 476, 'Kauno Apskritis'),
('en_US', 477, 'Klaipėdos Apskritis'),
('en_US', 478, 'Marijampolės Apskritis'),
('en_US', 479, 'Panevėžio Apskritis'),
('en_US', 480, 'Šiaulių Apskritis'),
('en_US', 481, 'Tauragės Apskritis'),
('en_US', 482, 'Telšių Apskritis'),
('en_US', 483, 'Utenos Apskritis'),
('en_US', 484, 'Vilniaus Apskritis'),
('en_US', 485, 'Acre'),
('en_US', 486, 'Alagoas'),
('en_US', 487, 'Amapá'),
('en_US', 488, 'Amazonas'),
('en_US', 489, 'Bahia'),
('en_US', 490, 'Ceará'),
('en_US', 491, 'Espírito Santo'),
('en_US', 492, 'Goiás'),
('en_US', 493, 'Maranhão'),
('en_US', 494, 'Mato Grosso'),
('en_US', 495, 'Mato Grosso do Sul'),
('en_US', 496, 'Minas Gerais'),
('en_US', 497, 'Pará'),
('en_US', 498, 'Paraíba'),
('en_US', 499, 'Paraná'),
('en_US', 500, 'Pernambuco'),
('en_US', 501, 'Piauí'),
('en_US', 502, 'Rio de Janeiro'),
('en_US', 503, 'Rio Grande do Norte'),
('en_US', 504, 'Rio Grande do Sul'),
('en_US', 505, 'Rondônia'),
('en_US', 506, 'Roraima'),
('en_US', 507, 'Santa Catarina'),
('en_US', 508, 'São Paulo'),
('en_US', 509, 'Sergipe'),
('en_US', 510, 'Tocantins'),
('en_US', 511, 'Distrito Federal');

-- --------------------------------------------------------

--
-- Table structure for table `directory_currency_rate`
--

CREATE TABLE `directory_currency_rate` (
  `currency_from` varchar(3) NOT NULL COMMENT 'Currency Code Convert From',
  `currency_to` varchar(3) NOT NULL COMMENT 'Currency Code Convert To',
  `rate` decimal(24,12) NOT NULL DEFAULT '0.000000000000' COMMENT 'Currency Conversion Rate'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Directory Currency Rate';

--
-- Dumping data for table `directory_currency_rate`
--

INSERT INTO `directory_currency_rate` (`currency_from`, `currency_to`, `rate`) VALUES
('EUR', 'EUR', '1.000000000000'),
('EUR', 'USD', '1.415000000000'),
('USD', 'EUR', '0.706700000000'),
('USD', 'USD', '1.000000000000');

-- --------------------------------------------------------

--
-- Table structure for table `downloadable_link`
--

CREATE TABLE `downloadable_link` (
  `link_id` int(10) UNSIGNED NOT NULL COMMENT 'Link ID',
  `product_id` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Product ID',
  `sort_order` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Sort order',
  `number_of_downloads` int(11) DEFAULT NULL COMMENT 'Number of downloads',
  `is_shareable` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Shareable flag',
  `link_url` varchar(255) DEFAULT NULL COMMENT 'Link Url',
  `link_file` varchar(255) DEFAULT NULL COMMENT 'Link File',
  `link_type` varchar(20) DEFAULT NULL COMMENT 'Link Type',
  `sample_url` varchar(255) DEFAULT NULL COMMENT 'Sample Url',
  `sample_file` varchar(255) DEFAULT NULL COMMENT 'Sample File',
  `sample_type` varchar(20) DEFAULT NULL COMMENT 'Sample Type'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Downloadable Link Table';

-- --------------------------------------------------------

--
-- Table structure for table `downloadable_link_price`
--

CREATE TABLE `downloadable_link_price` (
  `price_id` int(10) UNSIGNED NOT NULL COMMENT 'Price ID',
  `link_id` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Link ID',
  `website_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Website ID',
  `price` decimal(12,4) NOT NULL DEFAULT '0.0000' COMMENT 'Price'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Downloadable Link Price Table';

-- --------------------------------------------------------

--
-- Table structure for table `downloadable_link_purchased`
--

CREATE TABLE `downloadable_link_purchased` (
  `purchased_id` int(10) UNSIGNED NOT NULL COMMENT 'Purchased ID',
  `order_id` int(10) UNSIGNED DEFAULT '0' COMMENT 'Order ID',
  `order_increment_id` varchar(50) DEFAULT NULL COMMENT 'Order Increment ID',
  `order_item_id` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Order Item ID',
  `created_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT 'Date of creation',
  `updated_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP COMMENT 'Date of modification',
  `customer_id` int(10) UNSIGNED DEFAULT '0' COMMENT 'Customer ID',
  `product_name` varchar(255) DEFAULT NULL COMMENT 'Product name',
  `product_sku` varchar(255) DEFAULT NULL COMMENT 'Product sku',
  `link_section_title` varchar(255) DEFAULT NULL COMMENT 'Link_section_title'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Downloadable Link Purchased Table';

-- --------------------------------------------------------

--
-- Table structure for table `downloadable_link_purchased_item`
--

CREATE TABLE `downloadable_link_purchased_item` (
  `item_id` int(10) UNSIGNED NOT NULL COMMENT 'Item ID',
  `purchased_id` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Purchased ID',
  `order_item_id` int(10) UNSIGNED DEFAULT '0' COMMENT 'Order Item ID',
  `product_id` int(10) UNSIGNED DEFAULT '0' COMMENT 'Product ID',
  `link_hash` varchar(255) DEFAULT NULL COMMENT 'Link hash',
  `number_of_downloads_bought` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Number of downloads bought',
  `number_of_downloads_used` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Number of downloads used',
  `link_id` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Link ID',
  `link_title` varchar(255) DEFAULT NULL COMMENT 'Link Title',
  `is_shareable` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Shareable Flag',
  `link_url` varchar(255) DEFAULT NULL COMMENT 'Link Url',
  `link_file` varchar(255) DEFAULT NULL COMMENT 'Link File',
  `link_type` varchar(255) DEFAULT NULL COMMENT 'Link Type',
  `status` varchar(50) DEFAULT NULL COMMENT 'Status',
  `created_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT 'Creation Time',
  `updated_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP COMMENT 'Update Time'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Downloadable Link Purchased Item Table';

-- --------------------------------------------------------

--
-- Table structure for table `downloadable_link_title`
--

CREATE TABLE `downloadable_link_title` (
  `title_id` int(10) UNSIGNED NOT NULL COMMENT 'Title ID',
  `link_id` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Link ID',
  `store_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Store ID',
  `title` varchar(255) DEFAULT NULL COMMENT 'Title'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Link Title Table';

-- --------------------------------------------------------

--
-- Table structure for table `downloadable_sample`
--

CREATE TABLE `downloadable_sample` (
  `sample_id` int(10) UNSIGNED NOT NULL COMMENT 'Sample ID',
  `product_id` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Product ID',
  `sample_url` varchar(255) DEFAULT NULL COMMENT 'Sample URL',
  `sample_file` varchar(255) DEFAULT NULL COMMENT 'Sample file',
  `sample_type` varchar(20) DEFAULT NULL COMMENT 'Sample Type',
  `sort_order` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Sort Order'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Downloadable Sample Table';

-- --------------------------------------------------------

--
-- Table structure for table `downloadable_sample_title`
--

CREATE TABLE `downloadable_sample_title` (
  `title_id` int(10) UNSIGNED NOT NULL COMMENT 'Title ID',
  `sample_id` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Sample ID',
  `store_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Store ID',
  `title` varchar(255) DEFAULT NULL COMMENT 'Title'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Downloadable Sample Title Table';

-- --------------------------------------------------------

--
-- Table structure for table `eav_attribute`
--

CREATE TABLE `eav_attribute` (
  `attribute_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Attribute Id',
  `entity_type_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Entity Type Id',
  `attribute_code` varchar(255) DEFAULT NULL COMMENT 'Attribute Code',
  `attribute_model` varchar(255) DEFAULT NULL COMMENT 'Attribute Model',
  `backend_model` varchar(255) DEFAULT NULL COMMENT 'Backend Model',
  `backend_type` varchar(8) NOT NULL DEFAULT 'static' COMMENT 'Backend Type',
  `backend_table` varchar(255) DEFAULT NULL COMMENT 'Backend Table',
  `frontend_model` varchar(255) DEFAULT NULL COMMENT 'Frontend Model',
  `frontend_input` varchar(50) DEFAULT NULL COMMENT 'Frontend Input',
  `frontend_label` varchar(255) DEFAULT NULL COMMENT 'Frontend Label',
  `frontend_class` varchar(255) DEFAULT NULL COMMENT 'Frontend Class',
  `source_model` varchar(255) DEFAULT NULL COMMENT 'Source Model',
  `is_required` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Defines Is Required',
  `is_user_defined` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Defines Is User Defined',
  `default_value` text COMMENT 'Default Value',
  `is_unique` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Defines Is Unique',
  `note` varchar(255) DEFAULT NULL COMMENT 'Note'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Eav Attribute';

--
-- Dumping data for table `eav_attribute`
--

INSERT INTO `eav_attribute` (`attribute_id`, `entity_type_id`, `attribute_code`, `attribute_model`, `backend_model`, `backend_type`, `backend_table`, `frontend_model`, `frontend_input`, `frontend_label`, `frontend_class`, `source_model`, `is_required`, `is_user_defined`, `default_value`, `is_unique`, `note`) VALUES
(1, 1, 'website_id', NULL, 'Magento\\Customer\\Model\\Customer\\Attribute\\Backend\\Website', 'static', NULL, NULL, 'select', 'Associate to Website', NULL, 'Magento\\Customer\\Model\\Customer\\Attribute\\Source\\Website', 1, 0, NULL, 0, NULL),
(2, 1, 'store_id', NULL, 'Magento\\Customer\\Model\\Customer\\Attribute\\Backend\\Store', 'static', NULL, NULL, 'select', 'Create In', NULL, 'Magento\\Customer\\Model\\Customer\\Attribute\\Source\\Store', 1, 0, NULL, 0, NULL),
(3, 1, 'created_in', NULL, NULL, 'static', NULL, NULL, 'text', 'Created From', NULL, NULL, 0, 0, NULL, 0, NULL),
(4, 1, 'prefix', NULL, NULL, 'static', NULL, NULL, 'text', 'Prefix', NULL, NULL, 0, 0, NULL, 0, NULL),
(5, 1, 'firstname', NULL, NULL, 'static', NULL, NULL, 'text', 'First Name', NULL, NULL, 1, 0, NULL, 0, NULL),
(6, 1, 'middlename', NULL, NULL, 'static', NULL, NULL, 'text', 'Middle Name/Initial', NULL, NULL, 0, 0, NULL, 0, NULL),
(7, 1, 'lastname', NULL, NULL, 'static', NULL, NULL, 'text', 'Last Name', NULL, NULL, 1, 0, NULL, 0, NULL),
(8, 1, 'suffix', NULL, NULL, 'static', NULL, NULL, 'text', 'Suffix', NULL, NULL, 0, 0, NULL, 0, NULL),
(9, 1, 'email', NULL, NULL, 'static', NULL, NULL, 'text', 'Email', NULL, NULL, 1, 0, NULL, 0, NULL),
(10, 1, 'group_id', NULL, NULL, 'static', NULL, NULL, 'select', 'Group', NULL, 'Magento\\Customer\\Model\\Customer\\Attribute\\Source\\Group', 1, 0, NULL, 0, NULL),
(11, 1, 'dob', NULL, 'Magento\\Eav\\Model\\Entity\\Attribute\\Backend\\Datetime', 'static', NULL, 'Magento\\Eav\\Model\\Entity\\Attribute\\Frontend\\Datetime', 'date', 'Date Of Birth', NULL, NULL, 0, 0, NULL, 0, NULL),
(12, 1, 'password_hash', NULL, 'Magento\\Customer\\Model\\Customer\\Attribute\\Backend\\Password', 'static', NULL, NULL, 'hidden', NULL, NULL, NULL, 0, 0, NULL, 0, NULL),
(13, 1, 'rp_token', NULL, NULL, 'static', NULL, NULL, 'hidden', NULL, NULL, NULL, 0, 0, NULL, 0, NULL),
(14, 1, 'rp_token_created_at', NULL, NULL, 'static', NULL, NULL, 'date', NULL, NULL, NULL, 0, 0, NULL, 0, NULL),
(15, 1, 'default_billing', NULL, 'Magento\\Customer\\Model\\Customer\\Attribute\\Backend\\Billing', 'static', NULL, NULL, 'text', 'Default Billing Address', NULL, NULL, 0, 0, NULL, 0, NULL),
(16, 1, 'default_shipping', NULL, 'Magento\\Customer\\Model\\Customer\\Attribute\\Backend\\Shipping', 'static', NULL, NULL, 'text', 'Default Shipping Address', NULL, NULL, 0, 0, NULL, 0, NULL),
(17, 1, 'taxvat', NULL, NULL, 'static', NULL, NULL, 'text', 'Tax/VAT Number', NULL, NULL, 0, 0, NULL, 0, NULL),
(18, 1, 'confirmation', NULL, NULL, 'static', NULL, NULL, 'text', 'Is Confirmed', NULL, NULL, 0, 0, NULL, 0, NULL),
(19, 1, 'created_at', NULL, NULL, 'static', NULL, NULL, 'date', 'Created At', NULL, NULL, 0, 0, NULL, 0, NULL),
(20, 1, 'gender', NULL, NULL, 'static', NULL, NULL, 'select', 'Gender', NULL, 'Magento\\Eav\\Model\\Entity\\Attribute\\Source\\Table', 0, 0, NULL, 0, NULL),
(21, 1, 'disable_auto_group_change', NULL, 'Magento\\Customer\\Model\\Attribute\\Backend\\Data\\Boolean', 'static', NULL, NULL, 'boolean', 'Disable Automatic Group Change Based on VAT ID', NULL, NULL, 0, 0, NULL, 0, NULL),
(22, 2, 'prefix', NULL, NULL, 'static', NULL, NULL, 'text', 'Prefix', NULL, NULL, 0, 0, NULL, 0, NULL),
(23, 2, 'firstname', NULL, NULL, 'static', NULL, NULL, 'text', 'First Name', NULL, NULL, 1, 0, NULL, 0, NULL),
(24, 2, 'middlename', NULL, NULL, 'static', NULL, NULL, 'text', 'Middle Name/Initial', NULL, NULL, 0, 0, NULL, 0, NULL),
(25, 2, 'lastname', NULL, NULL, 'static', NULL, NULL, 'text', 'Last Name', NULL, NULL, 1, 0, NULL, 0, NULL),
(26, 2, 'suffix', NULL, NULL, 'static', NULL, NULL, 'text', 'Suffix', NULL, NULL, 0, 0, NULL, 0, NULL),
(27, 2, 'company', NULL, NULL, 'static', NULL, NULL, 'text', 'Company', NULL, NULL, 0, 0, NULL, 0, NULL),
(28, 2, 'street', NULL, 'Magento\\Eav\\Model\\Entity\\Attribute\\Backend\\DefaultBackend', 'static', NULL, NULL, 'multiline', 'Street Address', NULL, NULL, 1, 0, NULL, 0, NULL),
(29, 2, 'city', NULL, NULL, 'static', NULL, NULL, 'text', 'City', NULL, NULL, 1, 0, NULL, 0, NULL),
(30, 2, 'country_id', NULL, NULL, 'static', NULL, NULL, 'select', 'Country', NULL, 'Magento\\Customer\\Model\\ResourceModel\\Address\\Attribute\\Source\\Country', 1, 0, NULL, 0, NULL),
(31, 2, 'region', NULL, 'Magento\\Customer\\Model\\ResourceModel\\Address\\Attribute\\Backend\\Region', 'static', NULL, NULL, 'text', 'State/Province', NULL, NULL, 0, 0, NULL, 0, NULL),
(32, 2, 'region_id', NULL, NULL, 'static', NULL, NULL, 'hidden', 'State/Province', NULL, 'Magento\\Customer\\Model\\ResourceModel\\Address\\Attribute\\Source\\Region', 0, 0, NULL, 0, NULL),
(33, 2, 'postcode', NULL, NULL, 'static', NULL, NULL, 'text', 'Zip/Postal Code', NULL, NULL, 0, 0, NULL, 0, NULL),
(34, 2, 'telephone', NULL, NULL, 'static', NULL, NULL, 'text', 'Phone Number', NULL, NULL, 1, 0, NULL, 0, NULL),
(35, 2, 'fax', NULL, NULL, 'static', NULL, NULL, 'text', 'Fax', NULL, NULL, 0, 0, NULL, 0, NULL),
(36, 2, 'vat_id', NULL, NULL, 'static', NULL, NULL, 'text', 'VAT number', NULL, NULL, 0, 0, NULL, 0, NULL),
(37, 2, 'vat_is_valid', NULL, NULL, 'static', NULL, NULL, 'text', 'VAT number validity', NULL, NULL, 0, 0, NULL, 0, NULL),
(38, 2, 'vat_request_id', NULL, NULL, 'static', NULL, NULL, 'text', 'VAT number validation request ID', NULL, NULL, 0, 0, NULL, 0, NULL),
(39, 2, 'vat_request_date', NULL, NULL, 'static', NULL, NULL, 'text', 'VAT number validation request date', NULL, NULL, 0, 0, NULL, 0, NULL),
(40, 2, 'vat_request_success', NULL, NULL, 'static', NULL, NULL, 'text', 'VAT number validation request success', NULL, NULL, 0, 0, NULL, 0, NULL),
(41, 1, 'updated_at', NULL, NULL, 'static', NULL, NULL, 'date', 'Updated At', NULL, NULL, 0, 0, NULL, 0, NULL),
(42, 3, 'name', NULL, NULL, 'varchar', NULL, NULL, 'text', 'Name', NULL, NULL, 1, 0, NULL, 0, NULL),
(43, 3, 'is_active', NULL, NULL, 'int', NULL, NULL, 'select', 'Is Active', NULL, 'Magento\\Eav\\Model\\Entity\\Attribute\\Source\\Boolean', 1, 0, NULL, 0, NULL),
(44, 3, 'description', NULL, NULL, 'text', NULL, NULL, 'textarea', 'Description', NULL, NULL, 0, 0, NULL, 0, NULL),
(45, 3, 'image', NULL, 'Magento\\Catalog\\Model\\Category\\Attribute\\Backend\\Image', 'varchar', NULL, NULL, 'image', 'Image', NULL, NULL, 0, 0, NULL, 0, NULL),
(46, 3, 'meta_title', NULL, NULL, 'varchar', NULL, NULL, 'text', 'Page Title', NULL, NULL, 0, 0, NULL, 0, NULL),
(47, 3, 'meta_keywords', NULL, NULL, 'text', NULL, NULL, 'textarea', 'Meta Keywords', NULL, NULL, 0, 0, NULL, 0, NULL),
(48, 3, 'meta_description', NULL, NULL, 'text', NULL, NULL, 'textarea', 'Meta Description', NULL, NULL, 0, 0, NULL, 0, NULL),
(49, 3, 'display_mode', NULL, NULL, 'varchar', NULL, NULL, 'select', 'Display Mode', NULL, 'Magento\\Catalog\\Model\\Category\\Attribute\\Source\\Mode', 0, 0, NULL, 0, NULL),
(50, 3, 'landing_page', NULL, NULL, 'int', NULL, NULL, 'select', 'CMS Block', NULL, 'Magento\\Catalog\\Model\\Category\\Attribute\\Source\\Page', 0, 0, NULL, 0, NULL),
(51, 3, 'is_anchor', NULL, NULL, 'int', NULL, NULL, 'select', 'Is Anchor', NULL, 'Magento\\Eav\\Model\\Entity\\Attribute\\Source\\Boolean', 0, 0, '1', 0, NULL),
(52, 3, 'path', NULL, NULL, 'static', NULL, NULL, 'text', 'Path', NULL, NULL, 0, 0, NULL, 0, NULL),
(53, 3, 'position', NULL, NULL, 'static', NULL, NULL, 'text', 'Position', NULL, NULL, 0, 0, NULL, 0, NULL),
(54, 3, 'all_children', NULL, NULL, 'text', NULL, NULL, 'text', NULL, NULL, NULL, 0, 0, NULL, 0, NULL),
(55, 3, 'path_in_store', NULL, NULL, 'text', NULL, NULL, 'text', NULL, NULL, NULL, 0, 0, NULL, 0, NULL),
(56, 3, 'children', NULL, NULL, 'text', NULL, NULL, 'text', NULL, NULL, NULL, 0, 0, NULL, 0, NULL),
(57, 3, 'custom_design', NULL, NULL, 'varchar', NULL, NULL, 'select', 'Custom Design', NULL, 'Magento\\Theme\\Model\\Theme\\Source\\Theme', 0, 0, NULL, 0, NULL),
(58, 3, 'custom_design_from', 'Magento\\Catalog\\Model\\ResourceModel\\Eav\\Attribute', 'Magento\\Catalog\\Model\\Attribute\\Backend\\Startdate', 'datetime', NULL, 'Magento\\Eav\\Model\\Entity\\Attribute\\Frontend\\Datetime', 'date', 'Active From', NULL, NULL, 0, 0, NULL, 0, NULL),
(59, 3, 'custom_design_to', NULL, 'Magento\\Eav\\Model\\Entity\\Attribute\\Backend\\Datetime', 'datetime', NULL, NULL, 'date', 'Active To', NULL, NULL, 0, 0, NULL, 0, NULL),
(60, 3, 'page_layout', NULL, NULL, 'varchar', NULL, NULL, 'select', 'Page Layout', NULL, 'Magento\\Catalog\\Model\\Category\\Attribute\\Source\\Layout', 0, 0, NULL, 0, NULL),
(61, 3, 'custom_layout_update', NULL, 'Magento\\Catalog\\Model\\Attribute\\Backend\\Customlayoutupdate', 'text', NULL, NULL, 'textarea', 'Custom Layout Update', NULL, NULL, 0, 0, NULL, 0, NULL),
(62, 3, 'level', NULL, NULL, 'static', NULL, NULL, 'text', 'Level', NULL, NULL, 0, 0, NULL, 0, NULL),
(63, 3, 'children_count', NULL, NULL, 'static', NULL, NULL, 'text', 'Children Count', NULL, NULL, 0, 0, NULL, 0, NULL),
(64, 3, 'available_sort_by', NULL, 'Magento\\Catalog\\Model\\Category\\Attribute\\Backend\\Sortby', 'text', NULL, NULL, 'multiselect', 'Available Product Listing Sort By', NULL, 'Magento\\Catalog\\Model\\Category\\Attribute\\Source\\Sortby', 1, 0, NULL, 0, NULL),
(65, 3, 'default_sort_by', NULL, 'Magento\\Catalog\\Model\\Category\\Attribute\\Backend\\Sortby', 'varchar', NULL, NULL, 'select', 'Default Product Listing Sort By', NULL, 'Magento\\Catalog\\Model\\Category\\Attribute\\Source\\Sortby', 1, 0, NULL, 0, NULL),
(66, 3, 'include_in_menu', NULL, NULL, 'int', NULL, NULL, 'select', 'Include in Navigation Menu', NULL, 'Magento\\Eav\\Model\\Entity\\Attribute\\Source\\Boolean', 1, 0, '1', 0, NULL),
(67, 3, 'custom_use_parent_settings', NULL, NULL, 'int', NULL, NULL, 'select', 'Use Parent Category Settings', NULL, 'Magento\\Eav\\Model\\Entity\\Attribute\\Source\\Boolean', 0, 0, NULL, 0, NULL),
(68, 3, 'custom_apply_to_products', NULL, NULL, 'int', NULL, NULL, 'select', 'Apply To Products', NULL, 'Magento\\Eav\\Model\\Entity\\Attribute\\Source\\Boolean', 0, 0, NULL, 0, NULL),
(69, 3, 'filter_price_range', NULL, NULL, 'decimal', NULL, NULL, 'text', 'Layered Navigation Price Step', NULL, NULL, 0, 0, NULL, 0, NULL),
(70, 4, 'name', NULL, NULL, 'varchar', NULL, NULL, 'text', 'Name', 'validate-length maximum-length-255', NULL, 1, 0, NULL, 0, NULL),
(71, 4, 'sku', NULL, 'Magento\\Catalog\\Model\\Product\\Attribute\\Backend\\Sku', 'static', NULL, NULL, 'text', 'SKU', 'validate-length maximum-length-64', NULL, 1, 0, NULL, 1, NULL),
(72, 4, 'description', NULL, NULL, 'text', NULL, NULL, 'textarea', 'Description', NULL, NULL, 0, 0, NULL, 0, NULL),
(73, 4, 'short_description', NULL, NULL, 'text', NULL, NULL, 'textarea', 'Short Description', NULL, NULL, 0, 0, NULL, 0, NULL),
(74, 4, 'price', NULL, 'Magento\\Catalog\\Model\\Product\\Attribute\\Backend\\Price', 'decimal', NULL, NULL, 'price', 'Price', NULL, NULL, 1, 0, NULL, 0, NULL),
(75, 4, 'special_price', NULL, 'Magento\\Catalog\\Model\\Product\\Attribute\\Backend\\Price', 'decimal', NULL, NULL, 'price', 'Special Price', NULL, NULL, 0, 0, NULL, 0, NULL),
(76, 4, 'special_from_date', NULL, 'Magento\\Catalog\\Model\\Attribute\\Backend\\Startdate', 'datetime', NULL, NULL, 'date', 'Special Price From Date', NULL, NULL, 0, 0, NULL, 0, NULL),
(77, 4, 'special_to_date', NULL, 'Magento\\Eav\\Model\\Entity\\Attribute\\Backend\\Datetime', 'datetime', NULL, NULL, 'date', 'Special Price To Date', NULL, NULL, 0, 0, NULL, 0, NULL),
(78, 4, 'cost', NULL, 'Magento\\Catalog\\Model\\Product\\Attribute\\Backend\\Price', 'decimal', NULL, NULL, 'price', 'Cost', NULL, NULL, 0, 1, NULL, 0, NULL),
(79, 4, 'weight', NULL, 'Magento\\Catalog\\Model\\Product\\Attribute\\Backend\\Weight', 'decimal', NULL, NULL, 'weight', 'Weight', NULL, NULL, 0, 0, NULL, 0, NULL),
(80, 4, 'manufacturer', NULL, NULL, 'int', NULL, NULL, 'select', 'Manufacturer', NULL, NULL, 0, 1, NULL, 0, NULL),
(81, 4, 'meta_title', NULL, NULL, 'varchar', NULL, NULL, 'text', 'Meta Title', NULL, NULL, 0, 0, NULL, 0, NULL),
(82, 4, 'meta_keyword', NULL, NULL, 'text', NULL, NULL, 'textarea', 'Meta Keywords', NULL, NULL, 0, 0, NULL, 0, NULL),
(83, 4, 'meta_description', NULL, NULL, 'varchar', NULL, NULL, 'textarea', 'Meta Description', NULL, NULL, 0, 0, NULL, 0, 'Maximum 255 chars'),
(84, 4, 'image', NULL, NULL, 'varchar', NULL, 'Magento\\Catalog\\Model\\Product\\Attribute\\Frontend\\Image', 'media_image', 'Base Image', NULL, NULL, 0, 0, NULL, 0, NULL),
(85, 4, 'small_image', NULL, NULL, 'varchar', NULL, 'Magento\\Catalog\\Model\\Product\\Attribute\\Frontend\\Image', 'media_image', 'Small Image', NULL, NULL, 0, 0, NULL, 0, NULL),
(86, 4, 'thumbnail', NULL, NULL, 'varchar', NULL, 'Magento\\Catalog\\Model\\Product\\Attribute\\Frontend\\Image', 'media_image', 'Thumbnail', NULL, NULL, 0, 0, NULL, 0, NULL),
(87, 4, 'media_gallery', NULL, 'Magento\\Catalog\\Model\\Product\\Attribute\\Backend\\Media', 'varchar', NULL, NULL, 'gallery', 'Media Gallery', NULL, NULL, 0, 0, NULL, 0, NULL),
(88, 4, 'old_id', NULL, NULL, 'int', NULL, NULL, 'text', NULL, NULL, NULL, 0, 0, NULL, 0, NULL),
(89, 4, 'tier_price', NULL, 'Magento\\Catalog\\Model\\Product\\Attribute\\Backend\\Tierprice', 'decimal', NULL, NULL, 'text', 'Tier Price', NULL, NULL, 0, 0, NULL, 0, NULL),
(90, 4, 'color', NULL, NULL, 'int', NULL, NULL, 'select', 'Color', NULL, NULL, 0, 1, '', 0, NULL),
(91, 4, 'news_from_date', NULL, 'Magento\\Catalog\\Model\\Attribute\\Backend\\Startdate', 'datetime', NULL, NULL, 'date', 'Set Product as New from Date', NULL, NULL, 0, 0, NULL, 0, NULL),
(92, 4, 'news_to_date', NULL, 'Magento\\Eav\\Model\\Entity\\Attribute\\Backend\\Datetime', 'datetime', NULL, NULL, 'date', 'Set Product as New to Date', NULL, NULL, 0, 0, NULL, 0, NULL),
(93, 4, 'gallery', NULL, NULL, 'varchar', NULL, NULL, 'gallery', 'Image Gallery', NULL, NULL, 0, 0, NULL, 0, NULL),
(94, 4, 'status', NULL, NULL, 'int', NULL, NULL, 'select', 'Status', NULL, 'Magento\\Catalog\\Model\\Product\\Attribute\\Source\\Status', 0, 0, '1', 0, NULL),
(95, 4, 'minimal_price', NULL, NULL, 'decimal', NULL, NULL, 'price', 'Minimal Price', NULL, NULL, 0, 0, NULL, 0, NULL),
(96, 4, 'visibility', NULL, NULL, 'int', NULL, NULL, 'select', 'Visibility', NULL, 'Magento\\Catalog\\Model\\Product\\Visibility', 0, 0, '4', 0, NULL),
(97, 4, 'custom_design', NULL, NULL, 'varchar', NULL, NULL, 'select', 'Custom Design', NULL, 'Magento\\Theme\\Model\\Theme\\Source\\Theme', 0, 0, NULL, 0, NULL),
(98, 4, 'custom_design_from', NULL, 'Magento\\Catalog\\Model\\Attribute\\Backend\\Startdate', 'datetime', NULL, NULL, 'date', 'Active From', NULL, NULL, 0, 0, NULL, 0, NULL),
(99, 4, 'custom_design_to', NULL, 'Magento\\Eav\\Model\\Entity\\Attribute\\Backend\\Datetime', 'datetime', NULL, NULL, 'date', 'Active To', NULL, NULL, 0, 0, NULL, 0, NULL),
(100, 4, 'custom_layout_update', NULL, 'Magento\\Catalog\\Model\\Attribute\\Backend\\Customlayoutupdate', 'text', NULL, NULL, 'textarea', 'Custom Layout Update', NULL, NULL, 0, 0, NULL, 0, NULL),
(101, 4, 'page_layout', NULL, NULL, 'varchar', NULL, NULL, 'select', 'Page Layout', NULL, 'Magento\\Catalog\\Model\\Product\\Attribute\\Source\\Layout', 0, 0, NULL, 0, NULL),
(102, 4, 'category_ids', NULL, 'Magento\\Catalog\\Model\\Product\\Attribute\\Backend\\Category', 'static', NULL, NULL, 'text', 'Categories', NULL, NULL, 0, 0, NULL, 0, NULL),
(103, 4, 'options_container', NULL, NULL, 'varchar', NULL, NULL, 'select', 'Display Product Options In', NULL, 'Magento\\Catalog\\Model\\Entity\\Product\\Attribute\\Design\\Options\\Container', 0, 0, 'container2', 0, NULL),
(104, 4, 'required_options', NULL, NULL, 'static', NULL, NULL, 'text', NULL, NULL, NULL, 0, 0, NULL, 0, NULL),
(105, 4, 'has_options', NULL, NULL, 'static', NULL, NULL, 'text', NULL, NULL, NULL, 0, 0, NULL, 0, NULL),
(106, 4, 'image_label', NULL, NULL, 'varchar', NULL, NULL, 'text', 'Image Label', NULL, NULL, 0, 0, NULL, 0, NULL),
(107, 4, 'small_image_label', NULL, NULL, 'varchar', NULL, NULL, 'text', 'Small Image Label', NULL, NULL, 0, 0, NULL, 0, NULL),
(108, 4, 'thumbnail_label', NULL, NULL, 'varchar', NULL, NULL, 'text', 'Thumbnail Label', NULL, NULL, 0, 0, NULL, 0, NULL),
(109, 4, 'created_at', NULL, NULL, 'static', NULL, NULL, 'date', NULL, NULL, NULL, 1, 0, NULL, 0, NULL),
(110, 4, 'updated_at', NULL, NULL, 'static', NULL, NULL, 'date', NULL, NULL, NULL, 1, 0, NULL, 0, NULL),
(111, 4, 'country_of_manufacture', NULL, NULL, 'varchar', NULL, NULL, 'select', 'Country of Manufacture', NULL, 'Magento\\Catalog\\Model\\Product\\Attribute\\Source\\Countryofmanufacture', 0, 0, NULL, 0, NULL),
(112, 4, 'quantity_and_stock_status', NULL, 'Magento\\Catalog\\Model\\Product\\Attribute\\Backend\\Stock', 'int', NULL, NULL, 'select', 'Quantity', NULL, 'Magento\\CatalogInventory\\Model\\Source\\Stock', 0, 0, '1', 0, NULL),
(113, 3, 'url_key', NULL, NULL, 'varchar', NULL, NULL, 'text', 'URL Key', NULL, NULL, 0, 0, NULL, 0, NULL),
(114, 3, 'url_path', NULL, NULL, 'varchar', NULL, NULL, 'text', NULL, NULL, NULL, 0, 0, NULL, 0, NULL),
(115, 4, 'url_key', NULL, NULL, 'varchar', NULL, NULL, 'text', 'URL Key', NULL, NULL, 0, 0, NULL, 0, NULL),
(116, 4, 'url_path', NULL, NULL, 'varchar', NULL, NULL, 'text', NULL, NULL, NULL, 0, 0, NULL, 0, NULL),
(117, 4, 'msrp', NULL, 'Magento\\Catalog\\Model\\Product\\Attribute\\Backend\\Price', 'decimal', NULL, NULL, 'price', 'Manufacturer''s Suggested Retail Price', NULL, NULL, 0, 0, NULL, 0, NULL),
(118, 4, 'msrp_display_actual_price_type', NULL, 'Magento\\Catalog\\Model\\Product\\Attribute\\Backend\\Boolean', 'varchar', NULL, NULL, 'select', 'Display Actual Price', NULL, 'Magento\\Msrp\\Model\\Product\\Attribute\\Source\\Type\\Price', 0, 0, '0', 0, NULL),
(119, 4, 'price_type', NULL, NULL, 'int', NULL, NULL, NULL, NULL, NULL, NULL, 1, 0, NULL, 0, NULL),
(120, 4, 'sku_type', NULL, NULL, 'int', NULL, NULL, NULL, NULL, NULL, NULL, 1, 0, NULL, 0, NULL),
(121, 4, 'weight_type', NULL, NULL, 'int', NULL, NULL, NULL, NULL, NULL, NULL, 1, 0, NULL, 0, NULL),
(122, 4, 'price_view', NULL, NULL, 'int', NULL, NULL, 'select', 'Price View', NULL, 'Magento\\Bundle\\Model\\Product\\Attribute\\Source\\Price\\View', 1, 0, NULL, 0, NULL),
(123, 4, 'shipment_type', NULL, NULL, 'int', NULL, NULL, NULL, 'Shipment', NULL, NULL, 1, 0, NULL, 0, NULL),
(124, 4, 'links_purchased_separately', NULL, NULL, 'int', NULL, NULL, NULL, 'Links can be purchased separately', NULL, NULL, 1, 0, NULL, 0, NULL),
(125, 4, 'samples_title', NULL, NULL, 'varchar', NULL, NULL, NULL, 'Samples title', NULL, NULL, 1, 0, NULL, 0, NULL),
(126, 4, 'links_title', NULL, NULL, 'varchar', NULL, NULL, NULL, 'Links title', NULL, NULL, 1, 0, NULL, 0, NULL),
(127, 4, 'links_exist', NULL, NULL, 'int', NULL, NULL, NULL, NULL, NULL, NULL, 0, 0, '0', 0, NULL),
(128, 4, 'swatch_image', NULL, NULL, 'varchar', NULL, 'Magento\\Catalog\\Model\\Product\\Attribute\\Frontend\\Image', 'media_image', 'Swatch Image', NULL, NULL, 0, 0, NULL, 0, NULL),
(129, 4, 'tax_class_id', NULL, NULL, 'int', NULL, NULL, 'select', 'Tax Class', NULL, 'Magento\\Tax\\Model\\TaxClass\\Source\\Product', 0, 0, '2', 0, NULL),
(130, 4, 'gift_message_available', NULL, 'Magento\\Catalog\\Model\\Product\\Attribute\\Backend\\Boolean', 'varchar', NULL, NULL, 'select', 'Allow Gift Message', NULL, 'Magento\\Eav\\Model\\Entity\\Attribute\\Source\\Boolean', 0, 0, NULL, 0, NULL);

-- --------------------------------------------------------

--
-- Table structure for table `eav_attribute_group`
--

CREATE TABLE `eav_attribute_group` (
  `attribute_group_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Attribute Group Id',
  `attribute_set_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Attribute Set Id',
  `attribute_group_name` varchar(255) DEFAULT NULL COMMENT 'Attribute Group Name',
  `sort_order` smallint(6) NOT NULL DEFAULT '0' COMMENT 'Sort Order',
  `default_id` smallint(5) UNSIGNED DEFAULT '0' COMMENT 'Default Id',
  `attribute_group_code` varchar(255) NOT NULL COMMENT 'Attribute Group Code',
  `tab_group_code` varchar(255) DEFAULT NULL COMMENT 'Tab Group Code'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Eav Attribute Group';

--
-- Dumping data for table `eav_attribute_group`
--

INSERT INTO `eav_attribute_group` (`attribute_group_id`, `attribute_set_id`, `attribute_group_name`, `sort_order`, `default_id`, `attribute_group_code`, `tab_group_code`) VALUES
(1, 1, 'General', 1, 1, 'general', NULL),
(2, 2, 'General', 1, 1, 'general', NULL),
(3, 3, 'General', 10, 1, 'general', NULL),
(4, 3, 'General Information', 2, 0, 'general-information', NULL),
(5, 3, 'Display Settings', 20, 0, 'display-settings', NULL),
(6, 3, 'Custom Design', 30, 0, 'custom-design', NULL),
(7, 4, 'Product Details', 10, 1, 'product-details', 'basic'),
(8, 4, 'Advanced Pricing', 40, 0, 'advanced-pricing', 'advanced'),
(9, 4, 'Search Engine Optimization', 30, 0, 'search-engine-optimization', 'basic'),
(10, 4, 'Images and Videos', 20, 0, 'image-management', 'basic'),
(11, 4, 'Design', 50, 0, 'design', 'advanced'),
(12, 4, 'Autosettings', 60, 0, 'autosettings', 'advanced'),
(13, 5, 'General', 1, 1, 'general', NULL),
(14, 6, 'General', 1, 1, 'general', NULL),
(15, 7, 'General', 1, 1, 'general', NULL),
(16, 8, 'General', 1, 1, 'general', NULL);

-- --------------------------------------------------------

--
-- Table structure for table `eav_attribute_label`
--

CREATE TABLE `eav_attribute_label` (
  `attribute_label_id` int(10) UNSIGNED NOT NULL COMMENT 'Attribute Label Id',
  `attribute_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Attribute Id',
  `store_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Store Id',
  `value` varchar(255) DEFAULT NULL COMMENT 'Value'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Eav Attribute Label';

-- --------------------------------------------------------

--
-- Table structure for table `eav_attribute_option`
--

CREATE TABLE `eav_attribute_option` (
  `option_id` int(10) UNSIGNED NOT NULL COMMENT 'Option Id',
  `attribute_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Attribute Id',
  `sort_order` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Sort Order'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Eav Attribute Option';

--
-- Dumping data for table `eav_attribute_option`
--

INSERT INTO `eav_attribute_option` (`option_id`, `attribute_id`, `sort_order`) VALUES
(1, 20, 0),
(2, 20, 1),
(3, 20, 3),
(4, 90, 1),
(5, 90, 2),
(6, 90, 3);

-- --------------------------------------------------------

--
-- Table structure for table `eav_attribute_option_swatch`
--

CREATE TABLE `eav_attribute_option_swatch` (
  `swatch_id` int(10) UNSIGNED NOT NULL COMMENT 'Swatch ID',
  `option_id` int(10) UNSIGNED NOT NULL COMMENT 'Option ID',
  `store_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Store ID',
  `type` smallint(5) UNSIGNED NOT NULL COMMENT 'Swatch type: 0 - text, 1 - visual color, 2 - visual image',
  `value` varchar(255) DEFAULT NULL COMMENT 'Swatch Value'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Magento Swatches table';

-- --------------------------------------------------------

--
-- Table structure for table `eav_attribute_option_value`
--

CREATE TABLE `eav_attribute_option_value` (
  `value_id` int(10) UNSIGNED NOT NULL COMMENT 'Value Id',
  `option_id` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Option Id',
  `store_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Store Id',
  `value` varchar(255) DEFAULT NULL COMMENT 'Value'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Eav Attribute Option Value';

--
-- Dumping data for table `eav_attribute_option_value`
--

INSERT INTO `eav_attribute_option_value` (`value_id`, `option_id`, `store_id`, `value`) VALUES
(1, 1, 0, 'Male'),
(2, 2, 0, 'Female'),
(3, 3, 0, 'Not Specified'),
(4, 4, 0, 'blue'),
(5, 5, 0, 'pink'),
(6, 6, 0, 'red');

-- --------------------------------------------------------

--
-- Table structure for table `eav_attribute_set`
--

CREATE TABLE `eav_attribute_set` (
  `attribute_set_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Attribute Set Id',
  `entity_type_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Entity Type Id',
  `attribute_set_name` varchar(255) DEFAULT NULL COMMENT 'Attribute Set Name',
  `sort_order` smallint(6) NOT NULL DEFAULT '0' COMMENT 'Sort Order'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Eav Attribute Set';

--
-- Dumping data for table `eav_attribute_set`
--

INSERT INTO `eav_attribute_set` (`attribute_set_id`, `entity_type_id`, `attribute_set_name`, `sort_order`) VALUES
(1, 1, 'Default', 2),
(2, 2, 'Default', 2),
(3, 3, 'Default', 1),
(4, 4, 'Default', 1),
(5, 5, 'Default', 1),
(6, 6, 'Default', 1),
(7, 7, 'Default', 1),
(8, 8, 'Default', 1);

-- --------------------------------------------------------

--
-- Table structure for table `eav_entity`
--

CREATE TABLE `eav_entity` (
  `entity_id` int(10) UNSIGNED NOT NULL COMMENT 'Entity Id',
  `entity_type_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Entity Type Id',
  `attribute_set_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Attribute Set Id',
  `increment_id` varchar(50) DEFAULT NULL COMMENT 'Increment Id',
  `parent_id` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Parent Id',
  `store_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Store Id',
  `created_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT 'Created At',
  `updated_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP COMMENT 'Updated At',
  `is_active` smallint(5) UNSIGNED NOT NULL DEFAULT '1' COMMENT 'Defines Is Entity Active'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Eav Entity';

-- --------------------------------------------------------

--
-- Table structure for table `eav_entity_attribute`
--

CREATE TABLE `eav_entity_attribute` (
  `entity_attribute_id` int(10) UNSIGNED NOT NULL COMMENT 'Entity Attribute Id',
  `entity_type_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Entity Type Id',
  `attribute_set_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Attribute Set Id',
  `attribute_group_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Attribute Group Id',
  `attribute_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Attribute Id',
  `sort_order` smallint(6) NOT NULL DEFAULT '0' COMMENT 'Sort Order'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Eav Entity Attributes';

--
-- Dumping data for table `eav_entity_attribute`
--

INSERT INTO `eav_entity_attribute` (`entity_attribute_id`, `entity_type_id`, `attribute_set_id`, `attribute_group_id`, `attribute_id`, `sort_order`) VALUES
(1, 1, 1, 1, 1, 10),
(2, 1, 1, 1, 2, 20),
(3, 1, 1, 1, 3, 20),
(4, 1, 1, 1, 4, 30),
(5, 1, 1, 1, 5, 40),
(6, 1, 1, 1, 6, 50),
(7, 1, 1, 1, 7, 60),
(8, 1, 1, 1, 8, 70),
(9, 1, 1, 1, 9, 80),
(10, 1, 1, 1, 10, 25),
(11, 1, 1, 1, 11, 90),
(12, 1, 1, 1, 12, 81),
(13, 1, 1, 1, 13, 115),
(14, 1, 1, 1, 14, 120),
(15, 1, 1, 1, 15, 82),
(16, 1, 1, 1, 16, 83),
(17, 1, 1, 1, 17, 100),
(18, 1, 1, 1, 18, 85),
(19, 1, 1, 1, 19, 86),
(20, 1, 1, 1, 20, 110),
(21, 1, 1, 1, 21, 121),
(22, 2, 2, 2, 22, 10),
(23, 2, 2, 2, 23, 20),
(24, 2, 2, 2, 24, 30),
(25, 2, 2, 2, 25, 40),
(26, 2, 2, 2, 26, 50),
(27, 2, 2, 2, 27, 60),
(28, 2, 2, 2, 28, 70),
(29, 2, 2, 2, 29, 80),
(30, 2, 2, 2, 30, 90),
(31, 2, 2, 2, 31, 100),
(32, 2, 2, 2, 32, 100),
(33, 2, 2, 2, 33, 110),
(34, 2, 2, 2, 34, 120),
(35, 2, 2, 2, 35, 130),
(36, 2, 2, 2, 36, 131),
(37, 2, 2, 2, 37, 132),
(38, 2, 2, 2, 38, 133),
(39, 2, 2, 2, 39, 134),
(40, 2, 2, 2, 40, 135),
(41, 1, 1, 1, 41, 87),
(42, 3, 3, 4, 42, 1),
(43, 3, 3, 4, 43, 2),
(44, 3, 3, 4, 44, 4),
(45, 3, 3, 4, 45, 5),
(46, 3, 3, 4, 46, 6),
(47, 3, 3, 4, 47, 7),
(48, 3, 3, 4, 48, 8),
(49, 3, 3, 5, 49, 10),
(50, 3, 3, 5, 50, 20),
(51, 3, 3, 5, 51, 30),
(52, 3, 3, 4, 52, 12),
(53, 3, 3, 4, 53, 13),
(54, 3, 3, 4, 54, 14),
(55, 3, 3, 4, 55, 15),
(56, 3, 3, 4, 56, 16),
(57, 3, 3, 6, 57, 10),
(58, 3, 3, 6, 58, 30),
(59, 3, 3, 6, 59, 40),
(60, 3, 3, 6, 60, 50),
(61, 3, 3, 6, 61, 60),
(62, 3, 3, 4, 62, 24),
(63, 3, 3, 4, 63, 25),
(64, 3, 3, 5, 64, 40),
(65, 3, 3, 5, 65, 50),
(66, 3, 3, 4, 66, 10),
(67, 3, 3, 6, 67, 5),
(68, 3, 3, 6, 68, 6),
(69, 3, 3, 5, 69, 51),
(70, 4, 4, 7, 70, 10),
(71, 4, 4, 7, 71, 20),
(72, 4, 4, 7, 72, 90),
(73, 4, 4, 12, 73, 0),
(74, 4, 4, 7, 74, 30),
(75, 4, 4, 8, 75, 3),
(76, 4, 4, 8, 76, 4),
(77, 4, 4, 8, 77, 5),
(78, 4, 4, 8, 78, 6),
(79, 4, 4, 7, 79, 70),
(80, 4, 4, 9, 81, 20),
(81, 4, 4, 9, 82, 30),
(82, 4, 4, 9, 83, 40),
(83, 4, 4, 7, 84, 50),
(84, 4, 4, 10, 85, 2),
(85, 4, 4, 10, 86, 3),
(86, 4, 4, 10, 87, 4),
(87, 4, 4, 7, 88, 6),
(88, 4, 4, 8, 89, 7),
(89, 4, 4, 12, 91, 30),
(90, 4, 4, 12, 92, 40),
(91, 4, 4, 10, 93, 5),
(92, 4, 4, 7, 94, 100),
(93, 4, 4, 8, 95, 8),
(94, 4, 4, 12, 96, 20),
(95, 4, 4, 11, 97, 1),
(96, 4, 4, 11, 98, 2),
(97, 4, 4, 11, 99, 3),
(98, 4, 4, 11, 100, 4),
(99, 4, 4, 11, 101, 5),
(100, 4, 4, 7, 102, 80),
(101, 4, 4, 11, 103, 6),
(102, 4, 4, 7, 104, 14),
(103, 4, 4, 7, 105, 15),
(104, 4, 4, 7, 106, 16),
(105, 4, 4, 7, 107, 17),
(106, 4, 4, 7, 108, 18),
(107, 4, 4, 7, 109, 19),
(108, 4, 4, 7, 110, 20),
(109, 4, 4, 12, 111, 50),
(110, 4, 4, 7, 112, 60),
(111, 3, 3, 4, 113, 3),
(112, 3, 3, 4, 114, 17),
(113, 4, 4, 9, 115, 10),
(114, 4, 4, 7, 116, 11),
(115, 4, 4, 8, 117, 9),
(116, 4, 4, 8, 118, 10),
(117, 4, 4, 7, 119, 101),
(118, 4, 4, 7, 120, 102),
(119, 4, 4, 7, 121, 103),
(120, 4, 4, 8, 122, 11),
(121, 4, 4, 7, 123, 104),
(122, 4, 4, 7, 124, 105),
(123, 4, 4, 7, 125, 106),
(124, 4, 4, 7, 126, 107),
(125, 4, 4, 7, 127, 108),
(126, 4, 4, 7, 128, 3),
(127, 4, 4, 7, 129, 40),
(128, 4, 4, 12, 130, 60),
(130, 4, 4, 7, 90, 110);

-- --------------------------------------------------------

--
-- Table structure for table `eav_entity_datetime`
--

CREATE TABLE `eav_entity_datetime` (
  `value_id` int(11) NOT NULL COMMENT 'Value Id',
  `entity_type_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Entity Type Id',
  `attribute_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Attribute Id',
  `store_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Store Id',
  `entity_id` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Entity Id',
  `value` datetime DEFAULT NULL COMMENT 'Attribute Value'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Eav Entity Value Prefix';

-- --------------------------------------------------------

--
-- Table structure for table `eav_entity_decimal`
--

CREATE TABLE `eav_entity_decimal` (
  `value_id` int(11) NOT NULL COMMENT 'Value Id',
  `entity_type_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Entity Type Id',
  `attribute_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Attribute Id',
  `store_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Store Id',
  `entity_id` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Entity Id',
  `value` decimal(12,4) NOT NULL DEFAULT '0.0000' COMMENT 'Attribute Value'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Eav Entity Value Prefix';

-- --------------------------------------------------------

--
-- Table structure for table `eav_entity_int`
--

CREATE TABLE `eav_entity_int` (
  `value_id` int(11) NOT NULL COMMENT 'Value Id',
  `entity_type_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Entity Type Id',
  `attribute_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Attribute Id',
  `store_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Store Id',
  `entity_id` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Entity Id',
  `value` int(11) NOT NULL DEFAULT '0' COMMENT 'Attribute Value'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Eav Entity Value Prefix';

-- --------------------------------------------------------

--
-- Table structure for table `eav_entity_store`
--

CREATE TABLE `eav_entity_store` (
  `entity_store_id` int(10) UNSIGNED NOT NULL COMMENT 'Entity Store Id',
  `entity_type_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Entity Type Id',
  `store_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Store Id',
  `increment_prefix` varchar(20) DEFAULT NULL COMMENT 'Increment Prefix',
  `increment_last_id` varchar(50) DEFAULT NULL COMMENT 'Last Incremented Id'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Eav Entity Store';

-- --------------------------------------------------------

--
-- Table structure for table `eav_entity_text`
--

CREATE TABLE `eav_entity_text` (
  `value_id` int(11) NOT NULL COMMENT 'Value Id',
  `entity_type_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Entity Type Id',
  `attribute_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Attribute Id',
  `store_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Store Id',
  `entity_id` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Entity Id',
  `value` text NOT NULL COMMENT 'Attribute Value'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Eav Entity Value Prefix';

-- --------------------------------------------------------

--
-- Table structure for table `eav_entity_type`
--

CREATE TABLE `eav_entity_type` (
  `entity_type_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Entity Type Id',
  `entity_type_code` varchar(50) NOT NULL COMMENT 'Entity Type Code',
  `entity_model` varchar(255) NOT NULL COMMENT 'Entity Model',
  `attribute_model` varchar(255) DEFAULT NULL COMMENT 'Attribute Model',
  `entity_table` varchar(255) DEFAULT NULL COMMENT 'Entity Table',
  `value_table_prefix` varchar(255) DEFAULT NULL COMMENT 'Value Table Prefix',
  `entity_id_field` varchar(255) DEFAULT NULL COMMENT 'Entity Id Field',
  `is_data_sharing` smallint(5) UNSIGNED NOT NULL DEFAULT '1' COMMENT 'Defines Is Data Sharing',
  `data_sharing_key` varchar(100) DEFAULT 'default' COMMENT 'Data Sharing Key',
  `default_attribute_set_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Default Attribute Set Id',
  `increment_model` varchar(255) DEFAULT NULL COMMENT 'Increment Model',
  `increment_per_store` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Increment Per Store',
  `increment_pad_length` smallint(5) UNSIGNED NOT NULL DEFAULT '8' COMMENT 'Increment Pad Length',
  `increment_pad_char` varchar(1) NOT NULL DEFAULT '0' COMMENT 'Increment Pad Char',
  `additional_attribute_table` varchar(255) DEFAULT NULL COMMENT 'Additional Attribute Table',
  `entity_attribute_collection` varchar(255) DEFAULT NULL COMMENT 'Entity Attribute Collection'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Eav Entity Type';

--
-- Dumping data for table `eav_entity_type`
--

INSERT INTO `eav_entity_type` (`entity_type_id`, `entity_type_code`, `entity_model`, `attribute_model`, `entity_table`, `value_table_prefix`, `entity_id_field`, `is_data_sharing`, `data_sharing_key`, `default_attribute_set_id`, `increment_model`, `increment_per_store`, `increment_pad_length`, `increment_pad_char`, `additional_attribute_table`, `entity_attribute_collection`) VALUES
(1, 'customer', 'Magento\\Customer\\Model\\ResourceModel\\Customer', 'Magento\\Customer\\Model\\Attribute', 'customer_entity', NULL, NULL, 1, 'default', 1, 'Magento\\Eav\\Model\\Entity\\Increment\\NumericValue', 0, 8, '0', 'customer_eav_attribute', 'Magento\\Customer\\Model\\ResourceModel\\Attribute\\Collection'),
(2, 'customer_address', 'Magento\\Customer\\Model\\ResourceModel\\Address', 'Magento\\Customer\\Model\\Attribute', 'customer_address_entity', NULL, NULL, 1, 'default', 2, NULL, 0, 8, '0', 'customer_eav_attribute', 'Magento\\Customer\\Model\\ResourceModel\\Address\\Attribute\\Collection'),
(3, 'catalog_category', 'Magento\\Catalog\\Model\\ResourceModel\\Category', 'Magento\\Catalog\\Model\\ResourceModel\\Eav\\Attribute', 'catalog_category_entity', NULL, NULL, 1, 'default', 3, NULL, 0, 8, '0', 'catalog_eav_attribute', 'Magento\\Catalog\\Model\\ResourceModel\\Category\\Attribute\\Collection'),
(4, 'catalog_product', 'Magento\\Catalog\\Model\\ResourceModel\\Product', 'Magento\\Catalog\\Model\\ResourceModel\\Eav\\Attribute', 'catalog_product_entity', NULL, NULL, 1, 'default', 4, NULL, 0, 8, '0', 'catalog_eav_attribute', 'Magento\\Catalog\\Model\\ResourceModel\\Product\\Attribute\\Collection'),
(5, 'order', 'Magento\\Sales\\Model\\ResourceModel\\Order', NULL, 'sales_order', NULL, NULL, 1, 'default', 5, 'Magento\\Eav\\Model\\Entity\\Increment\\NumericValue', 1, 8, '0', NULL, NULL),
(6, 'invoice', 'Magento\\Sales\\Model\\ResourceModel\\Order', NULL, 'sales_invoice', NULL, NULL, 1, 'default', 6, 'Magento\\Eav\\Model\\Entity\\Increment\\NumericValue', 1, 8, '0', NULL, NULL),
(7, 'creditmemo', 'Magento\\Sales\\Model\\ResourceModel\\Order\\Creditmemo', NULL, 'sales_creditmemo', NULL, NULL, 1, 'default', 7, 'Magento\\Eav\\Model\\Entity\\Increment\\NumericValue', 1, 8, '0', NULL, NULL),
(8, 'shipment', 'Magento\\Sales\\Model\\ResourceModel\\Order\\Shipment', NULL, 'sales_shipment', NULL, NULL, 1, 'default', 8, 'Magento\\Eav\\Model\\Entity\\Increment\\NumericValue', 1, 8, '0', NULL, NULL);

-- --------------------------------------------------------

--
-- Table structure for table `eav_entity_varchar`
--

CREATE TABLE `eav_entity_varchar` (
  `value_id` int(11) NOT NULL COMMENT 'Value Id',
  `entity_type_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Entity Type Id',
  `attribute_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Attribute Id',
  `store_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Store Id',
  `entity_id` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Entity Id',
  `value` varchar(255) DEFAULT NULL COMMENT 'Attribute Value'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Eav Entity Value Prefix';

-- --------------------------------------------------------

--
-- Table structure for table `eav_form_element`
--

CREATE TABLE `eav_form_element` (
  `element_id` int(10) UNSIGNED NOT NULL COMMENT 'Element Id',
  `type_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Type Id',
  `fieldset_id` smallint(5) UNSIGNED DEFAULT NULL COMMENT 'Fieldset Id',
  `attribute_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Attribute Id',
  `sort_order` int(11) NOT NULL DEFAULT '0' COMMENT 'Sort Order'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Eav Form Element';

--
-- Dumping data for table `eav_form_element`
--

INSERT INTO `eav_form_element` (`element_id`, `type_id`, `fieldset_id`, `attribute_id`, `sort_order`) VALUES
(1, 1, NULL, 23, 0),
(2, 1, NULL, 25, 1),
(3, 1, NULL, 27, 2),
(4, 1, NULL, 9, 3),
(5, 1, NULL, 28, 4),
(6, 1, NULL, 29, 5),
(7, 1, NULL, 31, 6),
(8, 1, NULL, 33, 7),
(9, 1, NULL, 30, 8),
(10, 1, NULL, 34, 9),
(11, 1, NULL, 35, 10),
(12, 2, NULL, 23, 0),
(13, 2, NULL, 25, 1),
(14, 2, NULL, 27, 2),
(15, 2, NULL, 9, 3),
(16, 2, NULL, 28, 4),
(17, 2, NULL, 29, 5),
(18, 2, NULL, 31, 6),
(19, 2, NULL, 33, 7),
(20, 2, NULL, 30, 8),
(21, 2, NULL, 34, 9),
(22, 2, NULL, 35, 10),
(23, 3, NULL, 23, 0),
(24, 3, NULL, 25, 1),
(25, 3, NULL, 27, 2),
(26, 3, NULL, 28, 3),
(27, 3, NULL, 29, 4),
(28, 3, NULL, 31, 5),
(29, 3, NULL, 33, 6),
(30, 3, NULL, 30, 7),
(31, 3, NULL, 34, 8),
(32, 3, NULL, 35, 9),
(33, 4, NULL, 23, 0),
(34, 4, NULL, 25, 1),
(35, 4, NULL, 27, 2),
(36, 4, NULL, 28, 3),
(37, 4, NULL, 29, 4),
(38, 4, NULL, 31, 5),
(39, 4, NULL, 33, 6),
(40, 4, NULL, 30, 7),
(41, 4, NULL, 34, 8),
(42, 4, NULL, 35, 9);

-- --------------------------------------------------------

--
-- Table structure for table `eav_form_fieldset`
--

CREATE TABLE `eav_form_fieldset` (
  `fieldset_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Fieldset Id',
  `type_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Type Id',
  `code` varchar(64) NOT NULL COMMENT 'Code',
  `sort_order` int(11) NOT NULL DEFAULT '0' COMMENT 'Sort Order'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Eav Form Fieldset';

-- --------------------------------------------------------

--
-- Table structure for table `eav_form_fieldset_label`
--

CREATE TABLE `eav_form_fieldset_label` (
  `fieldset_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Fieldset Id',
  `store_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Store Id',
  `label` varchar(255) NOT NULL COMMENT 'Label'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Eav Form Fieldset Label';

-- --------------------------------------------------------

--
-- Table structure for table `eav_form_type`
--

CREATE TABLE `eav_form_type` (
  `type_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Type Id',
  `code` varchar(64) NOT NULL COMMENT 'Code',
  `label` varchar(255) NOT NULL COMMENT 'Label',
  `is_system` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Is System',
  `theme` varchar(64) DEFAULT NULL COMMENT 'Theme',
  `store_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Store Id'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Eav Form Type';

--
-- Dumping data for table `eav_form_type`
--

INSERT INTO `eav_form_type` (`type_id`, `code`, `label`, `is_system`, `theme`, `store_id`) VALUES
(1, 'checkout_onepage_register', 'checkout_onepage_register', 1, '', 0),
(2, 'checkout_onepage_register_guest', 'checkout_onepage_register_guest', 1, '', 0),
(3, 'checkout_onepage_billing_address', 'checkout_onepage_billing_address', 1, '', 0),
(4, 'checkout_onepage_shipping_address', 'checkout_onepage_shipping_address', 1, '', 0);

-- --------------------------------------------------------

--
-- Table structure for table `eav_form_type_entity`
--

CREATE TABLE `eav_form_type_entity` (
  `type_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Type Id',
  `entity_type_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Entity Type Id'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Eav Form Type Entity';

--
-- Dumping data for table `eav_form_type_entity`
--

INSERT INTO `eav_form_type_entity` (`type_id`, `entity_type_id`) VALUES
(1, 1),
(1, 2),
(2, 1),
(2, 2),
(3, 2),
(4, 2);

-- --------------------------------------------------------

--
-- Table structure for table `email_template`
--

CREATE TABLE `email_template` (
  `template_id` int(10) UNSIGNED NOT NULL COMMENT 'Template ID',
  `template_code` varchar(150) NOT NULL COMMENT 'Template Name',
  `template_text` text NOT NULL COMMENT 'Template Content',
  `template_styles` text COMMENT 'Templste Styles',
  `template_type` int(10) UNSIGNED DEFAULT NULL COMMENT 'Template Type',
  `template_subject` varchar(200) NOT NULL COMMENT 'Template Subject',
  `template_sender_name` varchar(200) DEFAULT NULL COMMENT 'Template Sender Name',
  `template_sender_email` varchar(200) DEFAULT NULL COMMENT 'Template Sender Email',
  `added_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT 'Date of Template Creation',
  `modified_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP COMMENT 'Date of Template Modification',
  `orig_template_code` varchar(200) DEFAULT NULL COMMENT 'Original Template Code',
  `orig_template_variables` text COMMENT 'Original Template Variables'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Email Templates';

-- --------------------------------------------------------

--
-- Table structure for table `flag`
--

CREATE TABLE `flag` (
  `flag_id` int(10) UNSIGNED NOT NULL COMMENT 'Flag Id',
  `flag_code` varchar(255) NOT NULL COMMENT 'Flag Code',
  `state` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Flag State',
  `flag_data` text COMMENT 'Flag Data',
  `last_update` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP COMMENT 'Date of Last Flag Update'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Flag';

-- --------------------------------------------------------

--
-- Table structure for table `gift_message`
--

CREATE TABLE `gift_message` (
  `gift_message_id` int(10) UNSIGNED NOT NULL COMMENT 'GiftMessage Id',
  `customer_id` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Customer id',
  `sender` varchar(255) DEFAULT NULL COMMENT 'Sender',
  `recipient` varchar(255) DEFAULT NULL COMMENT 'Registrant',
  `message` text COMMENT 'Message'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Gift Message';

-- --------------------------------------------------------

--
-- Table structure for table `googleoptimizer_code`
--

CREATE TABLE `googleoptimizer_code` (
  `code_id` int(10) UNSIGNED NOT NULL COMMENT 'Google experiment code id',
  `entity_id` int(10) UNSIGNED NOT NULL COMMENT 'Optimized entity id product id or catalog id',
  `entity_type` varchar(50) DEFAULT NULL COMMENT 'Optimized entity type',
  `store_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Store id',
  `experiment_script` text COMMENT 'Google experiment script'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Google Experiment code';

-- --------------------------------------------------------

--
-- Table structure for table `importexport_importdata`
--

CREATE TABLE `importexport_importdata` (
  `id` int(10) UNSIGNED NOT NULL COMMENT 'Id',
  `entity` varchar(50) NOT NULL COMMENT 'Entity',
  `behavior` varchar(10) NOT NULL DEFAULT 'append' COMMENT 'Behavior',
  `data` longtext COMMENT 'Data'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Import Data Table';

-- --------------------------------------------------------

--
-- Table structure for table `import_history`
--

CREATE TABLE `import_history` (
  `history_id` int(10) UNSIGNED NOT NULL COMMENT 'History record Id',
  `started_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT 'Started at',
  `user_id` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'User ID',
  `imported_file` varchar(255) DEFAULT NULL COMMENT 'Imported file',
  `execution_time` varchar(255) DEFAULT NULL COMMENT 'Execution time',
  `summary` varchar(255) DEFAULT NULL COMMENT 'Summary',
  `error_file` varchar(255) NOT NULL COMMENT 'Imported file with errors'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Import history table';

-- --------------------------------------------------------

--
-- Table structure for table `indexer_state`
--

CREATE TABLE `indexer_state` (
  `state_id` int(10) UNSIGNED NOT NULL COMMENT 'Indexer State Id',
  `indexer_id` varchar(255) DEFAULT NULL COMMENT 'Indexer Id',
  `status` varchar(16) DEFAULT 'invalid' COMMENT 'Indexer Status',
  `updated` datetime DEFAULT NULL COMMENT 'Indexer Status',
  `hash_config` varchar(32) NOT NULL COMMENT 'Hash of indexer config'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Indexer State';

--
-- Dumping data for table `indexer_state`
--

INSERT INTO `indexer_state` (`state_id`, `indexer_id`, `status`, `updated`, `hash_config`) VALUES
(1, 'customer_grid', 'valid', '2016-04-29 04:22:34', '9b4506442a512a649dde7c6f25924134'),
(2, 'catalog_category_product', 'valid', '2016-04-29 04:22:35', '86038392fe878acd22d5650a99b4f9b3'),
(3, 'catalog_product_category', 'valid', '2016-04-29 04:22:35', '8fd6f9a1ec8741ce1c7984b549915e8e'),
(4, 'catalog_product_price', 'valid', '2016-04-29 04:22:38', '0dce29088c0563479f66b2a70ebf152b'),
(5, 'catalog_product_attribute', 'valid', '2016-04-29 04:22:38', '5ee6fe2540126b9b2c90c53fe25c4d9a'),
(6, 'cataloginventory_stock', 'valid', '2016-04-29 04:22:39', '030021373629a9e2b3b8ffcc92be9483'),
(7, 'catalogrule_rule', 'valid', '2016-04-29 04:22:39', '63676f01f658a0964f150347a6596a0a'),
(8, 'catalogrule_product', 'valid', '2016-04-29 04:22:39', 'f9512548ab97beef43ea393d4a6dc545'),
(9, 'catalogsearch_fulltext', 'valid', '2016-04-29 04:22:43', 'a959fbd517e02dc6c79ef261cc983c97');

-- --------------------------------------------------------

--
-- Table structure for table `integration`
--

CREATE TABLE `integration` (
  `integration_id` int(10) UNSIGNED NOT NULL COMMENT 'Integration ID',
  `name` varchar(255) NOT NULL COMMENT 'Integration name is displayed in the admin interface',
  `email` varchar(255) NOT NULL COMMENT 'Email address of the contact person',
  `endpoint` varchar(255) DEFAULT NULL COMMENT 'Endpoint for posting consumer credentials',
  `status` smallint(5) UNSIGNED NOT NULL COMMENT 'Integration status',
  `consumer_id` int(10) UNSIGNED DEFAULT NULL COMMENT 'Oauth consumer',
  `created_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT 'Creation Time',
  `updated_at` timestamp NOT NULL DEFAULT '0000-00-00 00:00:00' ON UPDATE CURRENT_TIMESTAMP COMMENT 'Update Time',
  `setup_type` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Integration type - manual or config file',
  `identity_link_url` varchar(255) DEFAULT NULL COMMENT 'Identity linking Url'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='integration';

-- --------------------------------------------------------

--
-- Table structure for table `layout_link`
--

CREATE TABLE `layout_link` (
  `layout_link_id` int(10) UNSIGNED NOT NULL COMMENT 'Link Id',
  `store_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Store Id',
  `theme_id` int(10) UNSIGNED NOT NULL COMMENT 'Theme id',
  `layout_update_id` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Layout Update Id',
  `is_temporary` tinyint(1) NOT NULL DEFAULT '0' COMMENT 'Defines whether Layout Update is Temporary'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Layout Link';

-- --------------------------------------------------------

--
-- Table structure for table `layout_update`
--

CREATE TABLE `layout_update` (
  `layout_update_id` int(10) UNSIGNED NOT NULL COMMENT 'Layout Update Id',
  `handle` varchar(255) DEFAULT NULL COMMENT 'Handle',
  `xml` text COMMENT 'Xml',
  `sort_order` smallint(6) NOT NULL DEFAULT '0' COMMENT 'Sort Order',
  `updated_at` timestamp NULL DEFAULT '0000-00-00 00:00:00' ON UPDATE CURRENT_TIMESTAMP COMMENT 'Last Update Timestamp'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Layout Updates';

-- --------------------------------------------------------

--
-- Table structure for table `mview_state`
--

CREATE TABLE `mview_state` (
  `state_id` int(10) UNSIGNED NOT NULL COMMENT 'View State Id',
  `view_id` varchar(255) DEFAULT NULL COMMENT 'View Id',
  `mode` varchar(16) DEFAULT 'disabled' COMMENT 'View Mode',
  `status` varchar(16) DEFAULT 'idle' COMMENT 'View Status',
  `updated` datetime DEFAULT NULL COMMENT 'View updated time',
  `version_id` int(10) UNSIGNED DEFAULT NULL COMMENT 'View Version Id'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='View State';

-- --------------------------------------------------------

--
-- Table structure for table `newsletter_problem`
--

CREATE TABLE `newsletter_problem` (
  `problem_id` int(10) UNSIGNED NOT NULL COMMENT 'Problem Id',
  `subscriber_id` int(10) UNSIGNED DEFAULT NULL COMMENT 'Subscriber Id',
  `queue_id` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Queue Id',
  `problem_error_code` int(10) UNSIGNED DEFAULT '0' COMMENT 'Problem Error Code',
  `problem_error_text` varchar(200) DEFAULT NULL COMMENT 'Problem Error Text'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Newsletter Problems';

-- --------------------------------------------------------

--
-- Table structure for table `newsletter_queue`
--

CREATE TABLE `newsletter_queue` (
  `queue_id` int(10) UNSIGNED NOT NULL COMMENT 'Queue Id',
  `template_id` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Template ID',
  `newsletter_type` int(11) DEFAULT NULL COMMENT 'Newsletter Type',
  `newsletter_text` text COMMENT 'Newsletter Text',
  `newsletter_styles` text COMMENT 'Newsletter Styles',
  `newsletter_subject` varchar(200) DEFAULT NULL COMMENT 'Newsletter Subject',
  `newsletter_sender_name` varchar(200) DEFAULT NULL COMMENT 'Newsletter Sender Name',
  `newsletter_sender_email` varchar(200) DEFAULT NULL COMMENT 'Newsletter Sender Email',
  `queue_status` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Queue Status',
  `queue_start_at` timestamp NULL DEFAULT NULL COMMENT 'Queue Start At',
  `queue_finish_at` timestamp NULL DEFAULT NULL COMMENT 'Queue Finish At'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Newsletter Queue';

-- --------------------------------------------------------

--
-- Table structure for table `newsletter_queue_link`
--

CREATE TABLE `newsletter_queue_link` (
  `queue_link_id` int(10) UNSIGNED NOT NULL COMMENT 'Queue Link Id',
  `queue_id` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Queue Id',
  `subscriber_id` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Subscriber Id',
  `letter_sent_at` timestamp NULL DEFAULT NULL COMMENT 'Letter Sent At'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Newsletter Queue Link';

-- --------------------------------------------------------

--
-- Table structure for table `newsletter_queue_store_link`
--

CREATE TABLE `newsletter_queue_store_link` (
  `queue_id` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Queue Id',
  `store_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Store Id'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Newsletter Queue Store Link';

-- --------------------------------------------------------

--
-- Table structure for table `newsletter_subscriber`
--

CREATE TABLE `newsletter_subscriber` (
  `subscriber_id` int(10) UNSIGNED NOT NULL COMMENT 'Subscriber Id',
  `store_id` smallint(5) UNSIGNED DEFAULT '0' COMMENT 'Store Id',
  `change_status_at` timestamp NULL DEFAULT NULL COMMENT 'Change Status At',
  `customer_id` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Customer Id',
  `subscriber_email` varchar(150) DEFAULT NULL COMMENT 'Subscriber Email',
  `subscriber_status` int(11) NOT NULL DEFAULT '0' COMMENT 'Subscriber Status',
  `subscriber_confirm_code` varchar(32) DEFAULT 'NULL' COMMENT 'Subscriber Confirm Code'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Newsletter Subscriber';

-- --------------------------------------------------------

--
-- Table structure for table `newsletter_template`
--

CREATE TABLE `newsletter_template` (
  `template_id` int(10) UNSIGNED NOT NULL COMMENT 'Template ID',
  `template_code` varchar(150) DEFAULT NULL COMMENT 'Template Code',
  `template_text` text COMMENT 'Template Text',
  `template_styles` text COMMENT 'Template Styles',
  `template_type` int(10) UNSIGNED DEFAULT NULL COMMENT 'Template Type',
  `template_subject` varchar(200) DEFAULT NULL COMMENT 'Template Subject',
  `template_sender_name` varchar(200) DEFAULT NULL COMMENT 'Template Sender Name',
  `template_sender_email` varchar(200) DEFAULT NULL COMMENT 'Template Sender Email',
  `template_actual` smallint(5) UNSIGNED DEFAULT '1' COMMENT 'Template Actual',
  `added_at` timestamp NULL DEFAULT NULL COMMENT 'Added At',
  `modified_at` timestamp NULL DEFAULT NULL COMMENT 'Modified At'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Newsletter Template';

-- --------------------------------------------------------

--
-- Table structure for table `oauth_consumer`
--

CREATE TABLE `oauth_consumer` (
  `entity_id` int(10) UNSIGNED NOT NULL COMMENT 'Entity Id',
  `created_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT 'Created At',
  `updated_at` timestamp NULL DEFAULT '0000-00-00 00:00:00' ON UPDATE CURRENT_TIMESTAMP COMMENT 'Updated At',
  `name` varchar(255) NOT NULL COMMENT 'Name of consumer',
  `key` varchar(32) NOT NULL COMMENT 'Key code',
  `secret` varchar(32) NOT NULL COMMENT 'Secret code',
  `callback_url` varchar(255) DEFAULT NULL COMMENT 'Callback URL',
  `rejected_callback_url` varchar(255) NOT NULL COMMENT 'Rejected callback URL'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='OAuth Consumers';

-- --------------------------------------------------------

--
-- Table structure for table `oauth_nonce`
--

CREATE TABLE `oauth_nonce` (
  `nonce` varchar(32) NOT NULL COMMENT 'Nonce String',
  `timestamp` int(10) UNSIGNED NOT NULL COMMENT 'Nonce Timestamp',
  `consumer_id` int(10) UNSIGNED NOT NULL COMMENT 'Consumer ID'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='OAuth Nonce';

-- --------------------------------------------------------

--
-- Table structure for table `oauth_token`
--

CREATE TABLE `oauth_token` (
  `entity_id` int(10) UNSIGNED NOT NULL COMMENT 'Entity ID',
  `consumer_id` int(10) UNSIGNED DEFAULT NULL COMMENT 'Oauth Consumer ID',
  `admin_id` int(10) UNSIGNED DEFAULT NULL COMMENT 'Admin user ID',
  `customer_id` int(10) UNSIGNED DEFAULT NULL COMMENT 'Customer user ID',
  `type` varchar(16) NOT NULL COMMENT 'Token Type',
  `token` varchar(32) NOT NULL COMMENT 'Token',
  `secret` varchar(32) NOT NULL COMMENT 'Token Secret',
  `verifier` varchar(32) DEFAULT NULL COMMENT 'Token Verifier',
  `callback_url` varchar(255) NOT NULL COMMENT 'Token Callback URL',
  `revoked` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Is Token revoked',
  `authorized` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Is Token authorized',
  `user_type` int(11) DEFAULT NULL COMMENT 'User type',
  `created_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT 'Token creation timestamp'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='OAuth Tokens';

-- --------------------------------------------------------

--
-- Table structure for table `oauth_token_request_log`
--

CREATE TABLE `oauth_token_request_log` (
  `log_id` int(10) UNSIGNED NOT NULL COMMENT 'Log Id',
  `user_name` varchar(255) NOT NULL COMMENT 'Customer email or admin login',
  `user_type` smallint(5) UNSIGNED NOT NULL COMMENT 'User type (admin or customer)',
  `failures_count` smallint(5) UNSIGNED DEFAULT '0' COMMENT 'Number of failed authentication attempts in a row',
  `lock_expires_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP COMMENT 'Lock expiration time'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Log of token request authentication failures.';

-- --------------------------------------------------------

--
-- Table structure for table `paypal_billing_agreement`
--

CREATE TABLE `paypal_billing_agreement` (
  `agreement_id` int(10) UNSIGNED NOT NULL COMMENT 'Agreement Id',
  `customer_id` int(10) UNSIGNED NOT NULL COMMENT 'Customer Id',
  `method_code` varchar(32) NOT NULL COMMENT 'Method Code',
  `reference_id` varchar(32) NOT NULL COMMENT 'Reference Id',
  `status` varchar(20) NOT NULL COMMENT 'Status',
  `created_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT 'Created At',
  `updated_at` timestamp NULL DEFAULT NULL COMMENT 'Updated At',
  `store_id` smallint(5) UNSIGNED DEFAULT NULL COMMENT 'Store Id',
  `agreement_label` varchar(255) DEFAULT NULL COMMENT 'Agreement Label'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Sales Billing Agreement';

-- --------------------------------------------------------

--
-- Table structure for table `paypal_billing_agreement_order`
--

CREATE TABLE `paypal_billing_agreement_order` (
  `agreement_id` int(10) UNSIGNED NOT NULL COMMENT 'Agreement Id',
  `order_id` int(10) UNSIGNED NOT NULL COMMENT 'Order Id'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Sales Billing Agreement Order';

-- --------------------------------------------------------

--
-- Table structure for table `paypal_cert`
--

CREATE TABLE `paypal_cert` (
  `cert_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Cert Id',
  `website_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Website Id',
  `content` text COMMENT 'Content',
  `updated_at` timestamp NULL DEFAULT NULL COMMENT 'Updated At'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Paypal Certificate Table';

-- --------------------------------------------------------

--
-- Table structure for table `paypal_payment_transaction`
--

CREATE TABLE `paypal_payment_transaction` (
  `transaction_id` int(10) UNSIGNED NOT NULL COMMENT 'Entity Id',
  `txn_id` varchar(100) DEFAULT NULL COMMENT 'Txn Id',
  `additional_information` blob COMMENT 'Additional Information',
  `created_at` timestamp NULL DEFAULT NULL COMMENT 'Created At'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='PayPal Payflow Link Payment Transaction';

-- --------------------------------------------------------

--
-- Table structure for table `paypal_settlement_report`
--

CREATE TABLE `paypal_settlement_report` (
  `report_id` int(10) UNSIGNED NOT NULL COMMENT 'Report Id',
  `report_date` timestamp NULL DEFAULT NULL COMMENT 'Report Date',
  `account_id` varchar(64) DEFAULT NULL COMMENT 'Account Id',
  `filename` varchar(24) DEFAULT NULL COMMENT 'Filename',
  `last_modified` timestamp NULL DEFAULT NULL COMMENT 'Last Modified'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Paypal Settlement Report Table';

-- --------------------------------------------------------

--
-- Table structure for table `paypal_settlement_report_row`
--

CREATE TABLE `paypal_settlement_report_row` (
  `row_id` int(10) UNSIGNED NOT NULL COMMENT 'Row Id',
  `report_id` int(10) UNSIGNED NOT NULL COMMENT 'Report Id',
  `transaction_id` varchar(19) DEFAULT NULL COMMENT 'Transaction Id',
  `invoice_id` varchar(127) DEFAULT NULL COMMENT 'Invoice Id',
  `paypal_reference_id` varchar(19) DEFAULT NULL COMMENT 'Paypal Reference Id',
  `paypal_reference_id_type` varchar(3) DEFAULT NULL COMMENT 'Paypal Reference Id Type',
  `transaction_event_code` varchar(5) DEFAULT NULL COMMENT 'Transaction Event Code',
  `transaction_initiation_date` timestamp NULL DEFAULT NULL COMMENT 'Transaction Initiation Date',
  `transaction_completion_date` timestamp NULL DEFAULT NULL COMMENT 'Transaction Completion Date',
  `transaction_debit_or_credit` varchar(2) NOT NULL DEFAULT 'CR' COMMENT 'Transaction Debit Or Credit',
  `gross_transaction_amount` decimal(20,6) NOT NULL DEFAULT '0.000000' COMMENT 'Gross Transaction Amount',
  `gross_transaction_currency` varchar(3) DEFAULT NULL COMMENT 'Gross Transaction Currency',
  `fee_debit_or_credit` varchar(2) DEFAULT NULL COMMENT 'Fee Debit Or Credit',
  `fee_amount` decimal(20,6) NOT NULL DEFAULT '0.000000' COMMENT 'Fee Amount',
  `fee_currency` varchar(3) DEFAULT NULL COMMENT 'Fee Currency',
  `custom_field` varchar(255) DEFAULT NULL COMMENT 'Custom Field',
  `consumer_id` varchar(127) DEFAULT NULL COMMENT 'Consumer Id',
  `payment_tracking_id` varchar(255) DEFAULT NULL COMMENT 'Payment Tracking ID',
  `store_id` varchar(50) DEFAULT NULL COMMENT 'Store ID'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Paypal Settlement Report Row Table';

-- --------------------------------------------------------

--
-- Table structure for table `persistent_session`
--

CREATE TABLE `persistent_session` (
  `persistent_id` int(10) UNSIGNED NOT NULL COMMENT 'Session id',
  `key` varchar(50) NOT NULL COMMENT 'Unique cookie key',
  `customer_id` int(10) UNSIGNED DEFAULT NULL COMMENT 'Customer id',
  `website_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Website ID',
  `info` text COMMENT 'Session Data',
  `updated_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP COMMENT 'Updated At'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Persistent Session';

-- --------------------------------------------------------

--
-- Table structure for table `product_alert_price`
--

CREATE TABLE `product_alert_price` (
  `alert_price_id` int(10) UNSIGNED NOT NULL COMMENT 'Product alert price id',
  `customer_id` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Customer id',
  `product_id` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Product id',
  `price` decimal(12,4) NOT NULL DEFAULT '0.0000' COMMENT 'Price amount',
  `website_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Website id',
  `add_date` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT 'Product alert add date',
  `last_send_date` timestamp NULL DEFAULT NULL COMMENT 'Product alert last send date',
  `send_count` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Product alert send count',
  `status` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Product alert status'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Product Alert Price';

-- --------------------------------------------------------

--
-- Table structure for table `product_alert_stock`
--

CREATE TABLE `product_alert_stock` (
  `alert_stock_id` int(10) UNSIGNED NOT NULL COMMENT 'Product alert stock id',
  `customer_id` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Customer id',
  `product_id` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Product id',
  `website_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Website id',
  `add_date` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT 'Product alert add date',
  `send_date` timestamp NULL DEFAULT NULL COMMENT 'Product alert send date',
  `send_count` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Send Count',
  `status` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Product alert status'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Product Alert Stock';

-- --------------------------------------------------------

--
-- Table structure for table `quote`
--

CREATE TABLE `quote` (
  `entity_id` int(10) UNSIGNED NOT NULL COMMENT 'Entity Id',
  `store_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Store Id',
  `created_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT 'Created At',
  `updated_at` timestamp NOT NULL DEFAULT '0000-00-00 00:00:00' ON UPDATE CURRENT_TIMESTAMP COMMENT 'Updated At',
  `converted_at` timestamp NULL DEFAULT NULL COMMENT 'Converted At',
  `is_active` smallint(5) UNSIGNED DEFAULT '1' COMMENT 'Is Active',
  `is_virtual` smallint(5) UNSIGNED DEFAULT '0' COMMENT 'Is Virtual',
  `is_multi_shipping` smallint(5) UNSIGNED DEFAULT '0' COMMENT 'Is Multi Shipping',
  `items_count` int(10) UNSIGNED DEFAULT '0' COMMENT 'Items Count',
  `items_qty` decimal(12,4) DEFAULT '0.0000' COMMENT 'Items Qty',
  `orig_order_id` int(10) UNSIGNED DEFAULT '0' COMMENT 'Orig Order Id',
  `store_to_base_rate` decimal(12,4) DEFAULT '0.0000' COMMENT 'Store To Base Rate',
  `store_to_quote_rate` decimal(12,4) DEFAULT '0.0000' COMMENT 'Store To Quote Rate',
  `base_currency_code` varchar(255) DEFAULT NULL COMMENT 'Base Currency Code',
  `store_currency_code` varchar(255) DEFAULT NULL COMMENT 'Store Currency Code',
  `quote_currency_code` varchar(255) DEFAULT NULL COMMENT 'Quote Currency Code',
  `grand_total` decimal(12,4) DEFAULT '0.0000' COMMENT 'Grand Total',
  `base_grand_total` decimal(12,4) DEFAULT '0.0000' COMMENT 'Base Grand Total',
  `checkout_method` varchar(255) DEFAULT NULL COMMENT 'Checkout Method',
  `customer_id` int(10) UNSIGNED DEFAULT NULL COMMENT 'Customer Id',
  `customer_tax_class_id` int(10) UNSIGNED DEFAULT NULL COMMENT 'Customer Tax Class Id',
  `customer_group_id` int(10) UNSIGNED DEFAULT '0' COMMENT 'Customer Group Id',
  `customer_email` varchar(255) DEFAULT NULL COMMENT 'Customer Email',
  `customer_prefix` varchar(40) DEFAULT NULL COMMENT 'Customer Prefix',
  `customer_firstname` varchar(255) DEFAULT NULL COMMENT 'Customer Firstname',
  `customer_middlename` varchar(40) DEFAULT NULL COMMENT 'Customer Middlename',
  `customer_lastname` varchar(255) DEFAULT NULL COMMENT 'Customer Lastname',
  `customer_suffix` varchar(40) DEFAULT NULL COMMENT 'Customer Suffix',
  `customer_dob` datetime DEFAULT NULL COMMENT 'Customer Dob',
  `customer_note` varchar(255) DEFAULT NULL COMMENT 'Customer Note',
  `customer_note_notify` smallint(5) UNSIGNED DEFAULT '1' COMMENT 'Customer Note Notify',
  `customer_is_guest` smallint(5) UNSIGNED DEFAULT '0' COMMENT 'Customer Is Guest',
  `remote_ip` varchar(32) DEFAULT NULL COMMENT 'Remote Ip',
  `applied_rule_ids` varchar(255) DEFAULT NULL COMMENT 'Applied Rule Ids',
  `reserved_order_id` varchar(64) DEFAULT NULL COMMENT 'Reserved Order Id',
  `password_hash` varchar(255) DEFAULT NULL COMMENT 'Password Hash',
  `coupon_code` varchar(255) DEFAULT NULL COMMENT 'Coupon Code',
  `global_currency_code` varchar(255) DEFAULT NULL COMMENT 'Global Currency Code',
  `base_to_global_rate` decimal(12,4) DEFAULT NULL COMMENT 'Base To Global Rate',
  `base_to_quote_rate` decimal(12,4) DEFAULT NULL COMMENT 'Base To Quote Rate',
  `customer_taxvat` varchar(255) DEFAULT NULL COMMENT 'Customer Taxvat',
  `customer_gender` varchar(255) DEFAULT NULL COMMENT 'Customer Gender',
  `subtotal` decimal(12,4) DEFAULT NULL COMMENT 'Subtotal',
  `base_subtotal` decimal(12,4) DEFAULT NULL COMMENT 'Base Subtotal',
  `subtotal_with_discount` decimal(12,4) DEFAULT NULL COMMENT 'Subtotal With Discount',
  `base_subtotal_with_discount` decimal(12,4) DEFAULT NULL COMMENT 'Base Subtotal With Discount',
  `is_changed` int(10) UNSIGNED DEFAULT NULL COMMENT 'Is Changed',
  `trigger_recollect` smallint(6) NOT NULL DEFAULT '0' COMMENT 'Trigger Recollect',
  `ext_shipping_info` text COMMENT 'Ext Shipping Info',
  `is_persistent` smallint(5) UNSIGNED DEFAULT '0' COMMENT 'Is Quote Persistent',
  `gift_message_id` int(11) DEFAULT NULL COMMENT 'Gift Message Id'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Sales Flat Quote';

--
-- Dumping data for table `quote`
--

INSERT INTO `quote` (`entity_id`, `store_id`, `created_at`, `updated_at`, `converted_at`, `is_active`, `is_virtual`, `is_multi_shipping`, `items_count`, `items_qty`, `orig_order_id`, `store_to_base_rate`, `store_to_quote_rate`, `base_currency_code`, `store_currency_code`, `quote_currency_code`, `grand_total`, `base_grand_total`, `checkout_method`, `customer_id`, `customer_tax_class_id`, `customer_group_id`, `customer_email`, `customer_prefix`, `customer_firstname`, `customer_middlename`, `customer_lastname`, `customer_suffix`, `customer_dob`, `customer_note`, `customer_note_notify`, `customer_is_guest`, `remote_ip`, `applied_rule_ids`, `reserved_order_id`, `password_hash`, `coupon_code`, `global_currency_code`, `base_to_global_rate`, `base_to_quote_rate`, `customer_taxvat`, `customer_gender`, `subtotal`, `base_subtotal`, `subtotal_with_discount`, `base_subtotal_with_discount`, `is_changed`, `trigger_recollect`, `ext_shipping_info`, `is_persistent`, `gift_message_id`) VALUES
(1, 1, '2016-04-19 07:27:41', '0000-00-00 00:00:00', NULL, 1, 1, 0, 1, '1.0000', 0, '0.0000', '0.0000', 'USD', 'USD', 'USD', '120.0000', '120.0000', NULL, NULL, 3, 0, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, 1, 0, '::1', NULL, NULL, NULL, NULL, 'USD', '1.0000', '1.0000', NULL, NULL, '120.0000', '120.0000', '120.0000', '120.0000', 1, 0, NULL, 0, NULL),
(2, 1, '2016-04-19 09:16:27', '0000-00-00 00:00:00', NULL, 1, 1, 0, 1, '1.0000', 0, '0.0000', '0.0000', 'USD', 'USD', 'USD', '25.0000', '25.0000', NULL, NULL, 3, 0, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, 1, 0, '::1', NULL, NULL, NULL, NULL, 'USD', '1.0000', '1.0000', NULL, NULL, '25.0000', '25.0000', '25.0000', '25.0000', 1, 0, NULL, 0, NULL),
(3, 1, '2016-04-20 08:49:35', '2016-04-20 09:01:20', NULL, 1, 0, 0, 3, '3.0000', 0, '0.0000', '0.0000', 'USD', 'USD', 'USD', '295.0000', '295.0000', NULL, NULL, 3, 0, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, 1, 0, '::1', NULL, NULL, NULL, NULL, 'USD', '1.0000', '1.0000', NULL, NULL, '295.0000', '295.0000', '295.0000', '295.0000', 1, 0, NULL, 0, NULL),
(4, 1, '2016-04-21 02:27:58', '0000-00-00 00:00:00', NULL, 1, 1, 0, 1, '1.0000', 0, '0.0000', '0.0000', 'USD', 'USD', 'USD', '120.0000', '120.0000', NULL, NULL, 3, 0, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, 1, 0, '::1', NULL, NULL, NULL, NULL, 'USD', '1.0000', '1.0000', NULL, NULL, '120.0000', '120.0000', '120.0000', '120.0000', 1, 0, NULL, 0, NULL),
(5, 1, '2016-04-25 04:01:13', '2016-04-25 04:01:25', NULL, 1, 0, 0, 2, '3.0000', 0, '0.0000', '0.0000', 'USD', 'USD', 'USD', '184.0000', '184.0000', NULL, NULL, 3, 0, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, 1, 0, '::1', NULL, NULL, NULL, NULL, 'USD', '1.0000', '1.0000', NULL, NULL, '184.0000', '184.0000', '184.0000', '184.0000', 1, 0, NULL, 0, NULL),
(6, 1, '2016-04-25 07:20:48', '2016-04-25 07:20:50', NULL, 1, 0, 0, 2, '2.0000', 0, '0.0000', '0.0000', 'USD', 'USD', 'USD', '175.0000', '175.0000', NULL, NULL, 3, 0, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, 1, 0, '::1', NULL, NULL, NULL, NULL, 'USD', '1.0000', '1.0000', NULL, NULL, '175.0000', '175.0000', '175.0000', '175.0000', 1, 0, NULL, 0, NULL),
(7, 1, '2016-04-27 08:08:24', '2016-04-27 08:10:40', NULL, 0, 1, 0, 1, '1.0000', 0, '0.0000', '0.0000', 'USD', 'USD', 'USD', '120.0000', '120.0000', 'guest', NULL, 3, 0, 'lieult84@gmail.com', NULL, NULL, NULL, NULL, NULL, NULL, NULL, 1, 1, '::1', NULL, '000000001', NULL, NULL, 'USD', '1.0000', '1.0000', NULL, NULL, '120.0000', '120.0000', '120.0000', '120.0000', 1, 0, NULL, 0, NULL),
(8, 1, '2016-04-27 08:11:20', '2016-04-27 08:13:34', NULL, 0, 1, 0, 1, '1.0000', 0, '0.0000', '0.0000', 'USD', 'USD', 'USD', '120.0000', '120.0000', 'guest', NULL, 3, 0, 'lieult84@gmail.com', NULL, NULL, NULL, NULL, NULL, NULL, NULL, 1, 1, '::1', NULL, '000000002', NULL, NULL, 'USD', '1.0000', '1.0000', NULL, NULL, '120.0000', '120.0000', '120.0000', '120.0000', 1, 0, NULL, 0, NULL),
(9, 1, '2016-04-27 08:13:46', '2016-04-27 08:15:58', NULL, 0, 1, 0, 2, '2.0000', 0, '0.0000', '0.0000', 'USD', 'USD', 'USD', '49.0000', '49.0000', 'guest', NULL, 3, 0, 'lieult84@gmail.com', NULL, NULL, NULL, NULL, NULL, NULL, NULL, 1, 1, '::1', NULL, '000000003', NULL, NULL, 'USD', '1.0000', '1.0000', NULL, NULL, '49.0000', '49.0000', '49.0000', '49.0000', 1, 0, NULL, 0, NULL),
(10, 1, '2016-04-27 09:56:29', '0000-00-00 00:00:00', NULL, 1, 0, 0, 1, '1.0000', 0, '0.0000', '0.0000', 'USD', 'USD', 'USD', '80.0000', '80.0000', NULL, NULL, 3, 0, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, 1, 0, '::1', NULL, NULL, NULL, NULL, 'USD', '1.0000', '1.0000', NULL, NULL, '80.0000', '80.0000', '80.0000', '80.0000', 1, 0, NULL, 0, NULL),
(11, 1, '2016-04-28 02:43:12', '2016-04-28 03:06:28', NULL, 0, 1, 0, 3, '3.0000', 0, '0.0000', '0.0000', 'USD', 'USD', 'USD', '169.0000', '169.0000', NULL, 2, 3, 1, 'lieult84@yahoo.com', NULL, 'Le', NULL, 'Lieu', NULL, NULL, NULL, 1, 0, '::1', NULL, '000000004', NULL, NULL, 'USD', '1.0000', '1.0000', NULL, NULL, '169.0000', '169.0000', '169.0000', '169.0000', 1, 0, NULL, 0, NULL),
(12, 1, '2016-04-28 03:12:29', '2016-04-29 08:23:02', NULL, 1, 0, 0, 6, '9.0000', 0, '0.0000', '0.0000', 'USD', 'USD', 'USD', '849.0000', '849.0000', NULL, 2, 3, 1, 'lieult84@yahoo.com', NULL, 'Le', NULL, 'Lieu', NULL, NULL, NULL, 1, 0, '::1', NULL, NULL, NULL, NULL, 'USD', '1.0000', '1.0000', NULL, NULL, '849.0000', '849.0000', '849.0000', '849.0000', 1, 0, NULL, 0, NULL);

-- --------------------------------------------------------

--
-- Table structure for table `quote_address`
--

CREATE TABLE `quote_address` (
  `address_id` int(10) UNSIGNED NOT NULL COMMENT 'Address Id',
  `quote_id` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Quote Id',
  `created_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT 'Created At',
  `updated_at` timestamp NOT NULL DEFAULT '0000-00-00 00:00:00' ON UPDATE CURRENT_TIMESTAMP COMMENT 'Updated At',
  `customer_id` int(10) UNSIGNED DEFAULT NULL COMMENT 'Customer Id',
  `save_in_address_book` smallint(6) DEFAULT '0' COMMENT 'Save In Address Book',
  `customer_address_id` int(10) UNSIGNED DEFAULT NULL COMMENT 'Customer Address Id',
  `address_type` varchar(10) DEFAULT NULL COMMENT 'Address Type',
  `email` varchar(255) DEFAULT NULL COMMENT 'Email',
  `prefix` varchar(40) DEFAULT NULL COMMENT 'Prefix',
  `firstname` varchar(20) DEFAULT NULL COMMENT 'Firstname',
  `middlename` varchar(20) DEFAULT NULL COMMENT 'Middlename',
  `lastname` varchar(20) DEFAULT NULL COMMENT 'Lastname',
  `suffix` varchar(40) DEFAULT NULL COMMENT 'Suffix',
  `company` varchar(255) DEFAULT NULL COMMENT 'Company',
  `street` varchar(255) DEFAULT NULL COMMENT 'Street',
  `city` varchar(40) DEFAULT NULL COMMENT 'City',
  `region` varchar(40) DEFAULT NULL COMMENT 'Region',
  `region_id` int(10) UNSIGNED DEFAULT NULL COMMENT 'Region Id',
  `postcode` varchar(20) DEFAULT NULL COMMENT 'Postcode',
  `country_id` varchar(30) DEFAULT NULL COMMENT 'Country Id',
  `telephone` varchar(20) DEFAULT NULL COMMENT 'Phone Number',
  `fax` varchar(20) DEFAULT NULL COMMENT 'Fax',
  `same_as_billing` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Same As Billing',
  `collect_shipping_rates` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Collect Shipping Rates',
  `shipping_method` varchar(40) DEFAULT NULL COMMENT 'Shipping Method',
  `shipping_description` varchar(255) DEFAULT NULL COMMENT 'Shipping Description',
  `weight` decimal(12,4) NOT NULL DEFAULT '0.0000' COMMENT 'Weight',
  `subtotal` decimal(12,4) NOT NULL DEFAULT '0.0000' COMMENT 'Subtotal',
  `base_subtotal` decimal(12,4) NOT NULL DEFAULT '0.0000' COMMENT 'Base Subtotal',
  `subtotal_with_discount` decimal(12,4) NOT NULL DEFAULT '0.0000' COMMENT 'Subtotal With Discount',
  `base_subtotal_with_discount` decimal(12,4) NOT NULL DEFAULT '0.0000' COMMENT 'Base Subtotal With Discount',
  `tax_amount` decimal(12,4) NOT NULL DEFAULT '0.0000' COMMENT 'Tax Amount',
  `base_tax_amount` decimal(12,4) NOT NULL DEFAULT '0.0000' COMMENT 'Base Tax Amount',
  `shipping_amount` decimal(12,4) NOT NULL DEFAULT '0.0000' COMMENT 'Shipping Amount',
  `base_shipping_amount` decimal(12,4) NOT NULL DEFAULT '0.0000' COMMENT 'Base Shipping Amount',
  `shipping_tax_amount` decimal(12,4) DEFAULT NULL COMMENT 'Shipping Tax Amount',
  `base_shipping_tax_amount` decimal(12,4) DEFAULT NULL COMMENT 'Base Shipping Tax Amount',
  `discount_amount` decimal(12,4) NOT NULL DEFAULT '0.0000' COMMENT 'Discount Amount',
  `base_discount_amount` decimal(12,4) NOT NULL DEFAULT '0.0000' COMMENT 'Base Discount Amount',
  `grand_total` decimal(12,4) NOT NULL DEFAULT '0.0000' COMMENT 'Grand Total',
  `base_grand_total` decimal(12,4) NOT NULL DEFAULT '0.0000' COMMENT 'Base Grand Total',
  `customer_notes` text COMMENT 'Customer Notes',
  `applied_taxes` text COMMENT 'Applied Taxes',
  `discount_description` varchar(255) DEFAULT NULL COMMENT 'Discount Description',
  `shipping_discount_amount` decimal(12,4) DEFAULT NULL COMMENT 'Shipping Discount Amount',
  `base_shipping_discount_amount` decimal(12,4) DEFAULT NULL COMMENT 'Base Shipping Discount Amount',
  `subtotal_incl_tax` decimal(12,4) DEFAULT NULL COMMENT 'Subtotal Incl Tax',
  `base_subtotal_total_incl_tax` decimal(12,4) DEFAULT NULL COMMENT 'Base Subtotal Total Incl Tax',
  `discount_tax_compensation_amount` decimal(12,4) DEFAULT NULL COMMENT 'Discount Tax Compensation Amount',
  `base_discount_tax_compensation_amount` decimal(12,4) DEFAULT NULL COMMENT 'Base Discount Tax Compensation Amount',
  `shipping_discount_tax_compensation_amount` decimal(12,4) DEFAULT NULL COMMENT 'Shipping Discount Tax Compensation Amount',
  `base_shipping_discount_tax_compensation_amnt` decimal(12,4) DEFAULT NULL COMMENT 'Base Shipping Discount Tax Compensation Amount',
  `shipping_incl_tax` decimal(12,4) DEFAULT NULL COMMENT 'Shipping Incl Tax',
  `base_shipping_incl_tax` decimal(12,4) DEFAULT NULL COMMENT 'Base Shipping Incl Tax',
  `free_shipping` smallint(6) DEFAULT NULL,
  `vat_id` text COMMENT 'Vat Id',
  `vat_is_valid` smallint(6) DEFAULT NULL COMMENT 'Vat Is Valid',
  `vat_request_id` text COMMENT 'Vat Request Id',
  `vat_request_date` text COMMENT 'Vat Request Date',
  `vat_request_success` smallint(6) DEFAULT NULL COMMENT 'Vat Request Success',
  `gift_message_id` int(11) DEFAULT NULL COMMENT 'Gift Message Id'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Sales Flat Quote Address';

--
-- Dumping data for table `quote_address`
--

INSERT INTO `quote_address` (`address_id`, `quote_id`, `created_at`, `updated_at`, `customer_id`, `save_in_address_book`, `customer_address_id`, `address_type`, `email`, `prefix`, `firstname`, `middlename`, `lastname`, `suffix`, `company`, `street`, `city`, `region`, `region_id`, `postcode`, `country_id`, `telephone`, `fax`, `same_as_billing`, `collect_shipping_rates`, `shipping_method`, `shipping_description`, `weight`, `subtotal`, `base_subtotal`, `subtotal_with_discount`, `base_subtotal_with_discount`, `tax_amount`, `base_tax_amount`, `shipping_amount`, `base_shipping_amount`, `shipping_tax_amount`, `base_shipping_tax_amount`, `discount_amount`, `base_discount_amount`, `grand_total`, `base_grand_total`, `customer_notes`, `applied_taxes`, `discount_description`, `shipping_discount_amount`, `base_shipping_discount_amount`, `subtotal_incl_tax`, `base_subtotal_total_incl_tax`, `discount_tax_compensation_amount`, `base_discount_tax_compensation_amount`, `shipping_discount_tax_compensation_amount`, `base_shipping_discount_tax_compensation_amnt`, `shipping_incl_tax`, `base_shipping_incl_tax`, `free_shipping`, `vat_id`, `vat_is_valid`, `vat_request_id`, `vat_request_date`, `vat_request_success`, `gift_message_id`) VALUES
(1, 1, '2016-04-19 07:27:41', '0000-00-00 00:00:00', NULL, 0, NULL, 'billing', NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, 0, 0, NULL, NULL, '0.0000', '120.0000', '120.0000', '120.0000', '120.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '120.0000', '120.0000', NULL, 'a:0:{}', NULL, '0.0000', '0.0000', '120.0000', '120.0000', '0.0000', '0.0000', '0.0000', NULL, '0.0000', '0.0000', 0, NULL, NULL, NULL, NULL, NULL, NULL),
(2, 1, '2016-04-19 07:27:41', '0000-00-00 00:00:00', NULL, 0, NULL, 'shipping', NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, 1, 1, NULL, NULL, '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', NULL, NULL, '0.0000', '0.0000', '0.0000', '0.0000', NULL, 'N;', NULL, NULL, NULL, '0.0000', NULL, '0.0000', '0.0000', '0.0000', NULL, NULL, NULL, 0, NULL, NULL, NULL, NULL, NULL, NULL),
(3, 2, '2016-04-19 09:16:27', '0000-00-00 00:00:00', NULL, 0, NULL, 'billing', NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, 0, 0, NULL, NULL, '0.0000', '25.0000', '25.0000', '25.0000', '25.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '25.0000', '25.0000', NULL, 'a:0:{}', NULL, '0.0000', '0.0000', '25.0000', '25.0000', '0.0000', '0.0000', '0.0000', NULL, '0.0000', '0.0000', 0, NULL, NULL, NULL, NULL, NULL, NULL),
(4, 2, '2016-04-19 09:16:27', '0000-00-00 00:00:00', NULL, 0, NULL, 'shipping', NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, 1, 1, NULL, NULL, '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', NULL, NULL, '0.0000', '0.0000', '0.0000', '0.0000', NULL, 'N;', NULL, NULL, NULL, '0.0000', NULL, '0.0000', '0.0000', '0.0000', NULL, NULL, NULL, 0, NULL, NULL, NULL, NULL, NULL, NULL),
(5, 3, '2016-04-20 08:49:35', '0000-00-00 00:00:00', NULL, 0, NULL, 'billing', NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, 0, 0, NULL, NULL, '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', NULL, NULL, '0.0000', '0.0000', '0.0000', '0.0000', NULL, 'N;', NULL, NULL, NULL, '0.0000', NULL, '0.0000', '0.0000', '0.0000', NULL, NULL, NULL, 0, NULL, NULL, NULL, NULL, NULL, NULL),
(6, 3, '2016-04-20 08:49:35', '0000-00-00 00:00:00', NULL, 0, NULL, 'shipping', NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, 1, 0, NULL, NULL, '0.0000', '295.0000', '295.0000', '295.0000', '295.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '295.0000', '295.0000', NULL, 'a:0:{}', NULL, '0.0000', '0.0000', '295.0000', '295.0000', '0.0000', '0.0000', '0.0000', NULL, '0.0000', '0.0000', 0, NULL, NULL, NULL, NULL, NULL, NULL),
(7, 4, '2016-04-21 02:27:58', '0000-00-00 00:00:00', NULL, 0, NULL, 'billing', NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, 0, 0, NULL, NULL, '0.0000', '120.0000', '120.0000', '120.0000', '120.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '120.0000', '120.0000', NULL, 'a:0:{}', NULL, '0.0000', '0.0000', '120.0000', '120.0000', '0.0000', '0.0000', '0.0000', NULL, '0.0000', '0.0000', 0, NULL, NULL, NULL, NULL, NULL, NULL),
(8, 4, '2016-04-21 02:27:58', '0000-00-00 00:00:00', NULL, 0, NULL, 'shipping', NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, 1, 1, NULL, NULL, '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', NULL, NULL, '0.0000', '0.0000', '0.0000', '0.0000', NULL, 'N;', NULL, NULL, NULL, '0.0000', NULL, '0.0000', '0.0000', '0.0000', NULL, NULL, NULL, 0, NULL, NULL, NULL, NULL, NULL, NULL),
(9, 5, '2016-04-25 04:01:13', '0000-00-00 00:00:00', NULL, 0, NULL, 'billing', NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, 0, 0, NULL, NULL, '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', NULL, NULL, '0.0000', '0.0000', '0.0000', '0.0000', NULL, 'N;', NULL, NULL, NULL, '0.0000', NULL, '0.0000', '0.0000', '0.0000', NULL, NULL, NULL, 0, NULL, NULL, NULL, NULL, NULL, NULL),
(10, 5, '2016-04-25 04:01:13', '0000-00-00 00:00:00', NULL, 0, NULL, 'shipping', NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, 1, 0, NULL, NULL, '0.0000', '184.0000', '184.0000', '184.0000', '184.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '184.0000', '184.0000', NULL, 'a:0:{}', NULL, '0.0000', '0.0000', '184.0000', '184.0000', '0.0000', '0.0000', '0.0000', NULL, '0.0000', '0.0000', 0, NULL, NULL, NULL, NULL, NULL, NULL),
(11, 6, '2016-04-25 07:20:48', '0000-00-00 00:00:00', NULL, 0, NULL, 'billing', NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, 0, 0, NULL, NULL, '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', NULL, NULL, '0.0000', '0.0000', '0.0000', '0.0000', NULL, 'N;', NULL, NULL, NULL, '0.0000', NULL, '0.0000', '0.0000', '0.0000', NULL, NULL, NULL, 0, NULL, NULL, NULL, NULL, NULL, NULL),
(12, 6, '2016-04-25 07:20:48', '0000-00-00 00:00:00', NULL, 0, NULL, 'shipping', NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, 1, 0, NULL, NULL, '0.0000', '175.0000', '175.0000', '175.0000', '175.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '175.0000', '175.0000', NULL, 'a:0:{}', NULL, '0.0000', '0.0000', '175.0000', '175.0000', '0.0000', '0.0000', '0.0000', NULL, '0.0000', '0.0000', 0, NULL, NULL, NULL, NULL, NULL, NULL),
(13, 7, '2016-04-27 08:08:24', '0000-00-00 00:00:00', NULL, 1, NULL, 'billing', 'lieult84@gmail.com', NULL, 'Le', NULL, 'Lieu', NULL, 'Brainos', 'MD', 'Ha Noi', 'Alabama', 1, '12345', 'US', '123456789', NULL, 0, 0, NULL, NULL, '0.0000', '120.0000', '120.0000', '120.0000', '120.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '120.0000', '120.0000', NULL, 'a:0:{}', NULL, '0.0000', '0.0000', '120.0000', '120.0000', '0.0000', '0.0000', '0.0000', NULL, '0.0000', '0.0000', 0, NULL, NULL, NULL, NULL, NULL, NULL),
(14, 7, '2016-04-27 08:08:24', '0000-00-00 00:00:00', NULL, 0, NULL, 'shipping', NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, 1, 1, NULL, NULL, '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', NULL, NULL, '0.0000', '0.0000', '0.0000', '0.0000', NULL, 'N;', NULL, NULL, NULL, '0.0000', NULL, '0.0000', '0.0000', '0.0000', NULL, NULL, NULL, 0, NULL, NULL, NULL, NULL, NULL, NULL),
(15, 8, '2016-04-27 08:11:20', '0000-00-00 00:00:00', NULL, 1, NULL, 'billing', 'lieult84@gmail.com', NULL, 'Le ', NULL, 'Lieu', NULL, 'Brainos', 'MD', 'Ha Noi', 'Alabama', 1, '12345', 'US', '123456789', NULL, 0, 0, NULL, NULL, '0.0000', '120.0000', '120.0000', '120.0000', '120.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '120.0000', '120.0000', NULL, 'a:0:{}', NULL, '0.0000', '0.0000', '120.0000', '120.0000', '0.0000', '0.0000', '0.0000', NULL, '0.0000', '0.0000', 0, NULL, NULL, NULL, NULL, NULL, NULL),
(16, 8, '2016-04-27 08:11:20', '0000-00-00 00:00:00', NULL, 0, NULL, 'shipping', NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, 1, 1, NULL, NULL, '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', NULL, NULL, '0.0000', '0.0000', '0.0000', '0.0000', NULL, 'N;', NULL, NULL, NULL, '0.0000', NULL, '0.0000', '0.0000', '0.0000', NULL, NULL, NULL, 0, NULL, NULL, NULL, NULL, NULL, NULL),
(17, 9, '2016-04-27 08:13:46', '0000-00-00 00:00:00', NULL, 1, NULL, 'billing', 'lieult84@gmail.com', NULL, 'Le', NULL, 'Lieu', NULL, 'Brainos', 'MD', 'Ha Noi', 'Alabama', 1, '12345', 'US', '123456789', NULL, 0, 0, NULL, NULL, '0.0000', '49.0000', '49.0000', '49.0000', '49.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '49.0000', '49.0000', NULL, 'a:0:{}', NULL, '0.0000', '0.0000', '49.0000', '49.0000', '0.0000', '0.0000', '0.0000', NULL, '0.0000', '0.0000', 0, NULL, NULL, NULL, NULL, NULL, NULL),
(18, 9, '2016-04-27 08:13:46', '0000-00-00 00:00:00', NULL, 0, NULL, 'shipping', NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, 1, 1, NULL, NULL, '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', NULL, NULL, '0.0000', '0.0000', '0.0000', '0.0000', NULL, 'N;', NULL, NULL, NULL, '0.0000', NULL, '0.0000', '0.0000', '0.0000', NULL, NULL, NULL, 0, NULL, NULL, NULL, NULL, NULL, NULL),
(19, 10, '2016-04-27 09:56:29', '0000-00-00 00:00:00', NULL, 0, NULL, 'billing', NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, 0, 0, NULL, NULL, '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', NULL, NULL, '0.0000', '0.0000', '0.0000', '0.0000', NULL, 'N;', NULL, NULL, NULL, '0.0000', NULL, '0.0000', '0.0000', '0.0000', NULL, NULL, NULL, 0, NULL, NULL, NULL, NULL, NULL, NULL),
(20, 10, '2016-04-27 09:56:29', '0000-00-00 00:00:00', NULL, 0, NULL, 'shipping', NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, 1, 0, NULL, NULL, '0.0000', '80.0000', '80.0000', '80.0000', '80.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '80.0000', '80.0000', NULL, 'a:0:{}', NULL, '0.0000', '0.0000', '80.0000', '80.0000', '0.0000', '0.0000', '0.0000', NULL, '0.0000', '0.0000', 0, NULL, NULL, NULL, NULL, NULL, NULL),
(21, 11, '2016-04-28 02:43:12', '0000-00-00 00:00:00', 2, 1, NULL, 'billing', 'lieult84@yahoo.com', NULL, 'Le', NULL, 'Lieu', NULL, 'TNT', 'MD', 'Ha Noi', 'Alabama', 1, '12345', 'US', '123456789', NULL, 0, 0, NULL, NULL, '0.0000', '169.0000', '169.0000', '169.0000', '169.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '169.0000', '169.0000', NULL, 'a:0:{}', NULL, '0.0000', '0.0000', '169.0000', '169.0000', '0.0000', '0.0000', '0.0000', NULL, '0.0000', '0.0000', 0, NULL, NULL, NULL, NULL, NULL, NULL),
(22, 11, '2016-04-28 02:43:12', '0000-00-00 00:00:00', 2, 0, NULL, 'shipping', 'lieult84@yahoo.com', NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, 1, 1, NULL, NULL, '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', NULL, NULL, '0.0000', '0.0000', '0.0000', '0.0000', NULL, 'N;', NULL, NULL, NULL, '0.0000', NULL, '0.0000', '0.0000', '0.0000', NULL, NULL, NULL, 0, NULL, NULL, NULL, NULL, NULL, NULL),
(27, 12, '2016-04-29 08:15:46', '0000-00-00 00:00:00', 2, 0, 2, 'shipping', 'lieult84@yahoo.com', NULL, 'Le', NULL, 'Lieu', NULL, 'TNT', 'MD', 'Ha Noi', 'Alabama', 1, '12345', 'US', '123456789', NULL, 1, 0, NULL, NULL, '0.0000', '849.0000', '849.0000', '849.0000', '849.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '849.0000', '849.0000', NULL, 'a:0:{}', NULL, '0.0000', '0.0000', '849.0000', '849.0000', '0.0000', '0.0000', '0.0000', NULL, '0.0000', '0.0000', 0, NULL, NULL, NULL, NULL, NULL, NULL),
(28, 12, '2016-04-29 08:15:46', '0000-00-00 00:00:00', 2, 0, 2, 'billing', 'lieult84@yahoo.com', NULL, 'Le', NULL, 'Lieu', NULL, 'TNT', 'MD', 'Ha Noi', 'Alabama', 1, '12345', 'US', '123456789', NULL, 0, 0, NULL, NULL, '0.0000', '0.0000', '0.0000', '99.0000', '99.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', NULL, 'N;', NULL, '0.0000', '0.0000', '0.0000', '99.0000', '0.0000', '0.0000', '0.0000', NULL, '0.0000', '0.0000', 0, NULL, NULL, NULL, NULL, NULL, NULL);

-- --------------------------------------------------------

--
-- Table structure for table `quote_address_item`
--

CREATE TABLE `quote_address_item` (
  `address_item_id` int(10) UNSIGNED NOT NULL COMMENT 'Address Item Id',
  `parent_item_id` int(10) UNSIGNED DEFAULT NULL COMMENT 'Parent Item Id',
  `quote_address_id` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Quote Address Id',
  `quote_item_id` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Quote Item Id',
  `created_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT 'Created At',
  `updated_at` timestamp NOT NULL DEFAULT '0000-00-00 00:00:00' ON UPDATE CURRENT_TIMESTAMP COMMENT 'Updated At',
  `applied_rule_ids` text COMMENT 'Applied Rule Ids',
  `additional_data` text COMMENT 'Additional Data',
  `weight` decimal(12,4) DEFAULT '0.0000' COMMENT 'Weight',
  `qty` decimal(12,4) NOT NULL DEFAULT '0.0000' COMMENT 'Qty',
  `discount_amount` decimal(12,4) DEFAULT '0.0000' COMMENT 'Discount Amount',
  `tax_amount` decimal(12,4) DEFAULT '0.0000' COMMENT 'Tax Amount',
  `row_total` decimal(12,4) NOT NULL DEFAULT '0.0000' COMMENT 'Row Total',
  `base_row_total` decimal(12,4) NOT NULL DEFAULT '0.0000' COMMENT 'Base Row Total',
  `row_total_with_discount` decimal(12,4) DEFAULT '0.0000' COMMENT 'Row Total With Discount',
  `base_discount_amount` decimal(12,4) DEFAULT '0.0000' COMMENT 'Base Discount Amount',
  `base_tax_amount` decimal(12,4) DEFAULT '0.0000' COMMENT 'Base Tax Amount',
  `row_weight` decimal(12,4) DEFAULT '0.0000' COMMENT 'Row Weight',
  `product_id` int(10) UNSIGNED DEFAULT NULL COMMENT 'Product Id',
  `super_product_id` int(10) UNSIGNED DEFAULT NULL COMMENT 'Super Product Id',
  `parent_product_id` int(10) UNSIGNED DEFAULT NULL COMMENT 'Parent Product Id',
  `sku` varchar(255) DEFAULT NULL COMMENT 'Sku',
  `image` varchar(255) DEFAULT NULL COMMENT 'Image',
  `name` varchar(255) DEFAULT NULL COMMENT 'Name',
  `description` text COMMENT 'Description',
  `is_qty_decimal` int(10) UNSIGNED DEFAULT NULL COMMENT 'Is Qty Decimal',
  `price` decimal(12,4) DEFAULT NULL COMMENT 'Price',
  `discount_percent` decimal(12,4) DEFAULT NULL COMMENT 'Discount Percent',
  `no_discount` int(10) UNSIGNED DEFAULT NULL COMMENT 'No Discount',
  `tax_percent` decimal(12,4) DEFAULT NULL COMMENT 'Tax Percent',
  `base_price` decimal(12,4) DEFAULT NULL COMMENT 'Base Price',
  `base_cost` decimal(12,4) DEFAULT NULL COMMENT 'Base Cost',
  `price_incl_tax` decimal(12,4) DEFAULT NULL COMMENT 'Price Incl Tax',
  `base_price_incl_tax` decimal(12,4) DEFAULT NULL COMMENT 'Base Price Incl Tax',
  `row_total_incl_tax` decimal(12,4) DEFAULT NULL COMMENT 'Row Total Incl Tax',
  `base_row_total_incl_tax` decimal(12,4) DEFAULT NULL COMMENT 'Base Row Total Incl Tax',
  `discount_tax_compensation_amount` decimal(12,4) DEFAULT NULL COMMENT 'Discount Tax Compensation Amount',
  `base_discount_tax_compensation_amount` decimal(12,4) DEFAULT NULL COMMENT 'Base Discount Tax Compensation Amount',
  `free_shipping` int(11) DEFAULT NULL,
  `gift_message_id` int(11) DEFAULT NULL COMMENT 'Gift Message Id'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Sales Flat Quote Address Item';

--
-- Dumping data for table `quote_address_item`
--

INSERT INTO `quote_address_item` (`address_item_id`, `parent_item_id`, `quote_address_id`, `quote_item_id`, `created_at`, `updated_at`, `applied_rule_ids`, `additional_data`, `weight`, `qty`, `discount_amount`, `tax_amount`, `row_total`, `base_row_total`, `row_total_with_discount`, `base_discount_amount`, `base_tax_amount`, `row_weight`, `product_id`, `super_product_id`, `parent_product_id`, `sku`, `image`, `name`, `description`, `is_qty_decimal`, `price`, `discount_percent`, `no_discount`, `tax_percent`, `base_price`, `base_cost`, `price_incl_tax`, `base_price_incl_tax`, `row_total_incl_tax`, `base_row_total_incl_tax`, `discount_tax_compensation_amount`, `base_discount_tax_compensation_amount`, `free_shipping`, `gift_message_id`) VALUES
(1, NULL, 27, 25, '2016-04-29 08:15:46', '0000-00-00 00:00:00', NULL, NULL, NULL, '1.0000', '0.0000', '0.0000', '150.0000', '150.0000', '0.0000', '0.0000', '0.0000', '0.0000', 1, NULL, NULL, 'Ariel Roll Sleeve Sweatshirt', NULL, 'Ariel Roll Sleeve Sweatshirt', NULL, NULL, '150.0000', '0.0000', NULL, '0.0000', '150.0000', NULL, '150.0000', '150.0000', '150.0000', '150.0000', '0.0000', '0.0000', 0, NULL),
(2, NULL, 27, 31, '2016-04-29 08:15:46', '0000-00-00 00:00:00', NULL, NULL, NULL, '1.0000', '0.0000', '0.0000', '300.0000', '300.0000', '0.0000', '0.0000', '0.0000', '0.0000', 1, NULL, NULL, 'Ariel Roll Sleeve Sweatshirt', NULL, 'Ariel Roll Sleeve Sweatshirt', NULL, NULL, '150.0000', '0.0000', NULL, '0.0000', '150.0000', NULL, '150.0000', '150.0000', '300.0000', '300.0000', '0.0000', '0.0000', 0, NULL),
(3, NULL, 28, 26, '2016-04-29 08:15:46', '0000-00-00 00:00:00', NULL, NULL, NULL, '1.0000', '0.0000', '0.0000', '25.0000', '25.0000', '0.0000', '0.0000', '0.0000', '0.0000', 2, NULL, NULL, 'Arcadio Gym Short-32-Blue', NULL, 'Arcadio Gym Short-32-Blue', NULL, NULL, '25.0000', '0.0000', NULL, '0.0000', '25.0000', NULL, '25.0000', '25.0000', '25.0000', '25.0000', '0.0000', '0.0000', 0, NULL),
(4, NULL, 28, 32, '2016-04-29 08:15:46', '0000-00-00 00:00:00', NULL, NULL, NULL, '1.0000', '0.0000', '0.0000', '24.0000', '24.0000', '0.0000', '0.0000', '0.0000', '0.0000', 4, NULL, NULL, 'Arcadio Gym Short', NULL, 'Arcadio Gym Short', NULL, NULL, '24.0000', '0.0000', NULL, '0.0000', '24.0000', NULL, '24.0000', '24.0000', '24.0000', '24.0000', '0.0000', '0.0000', 0, NULL),
(5, NULL, 28, 33, '2016-04-29 08:15:46', '0000-00-00 00:00:00', NULL, NULL, NULL, '1.0000', '0.0000', '0.0000', '25.0000', '25.0000', '0.0000', '0.0000', '0.0000', '0.0000', 3, NULL, NULL, 'Atomic Endurance Running Tee', NULL, 'Atomic Endurance Running Tee', NULL, NULL, '25.0000', '0.0000', NULL, '0.0000', '25.0000', NULL, '25.0000', '25.0000', '25.0000', '25.0000', '0.0000', '0.0000', 0, NULL),
(6, NULL, 28, 34, '2016-04-29 08:15:46', '0000-00-00 00:00:00', NULL, NULL, NULL, '1.0000', '0.0000', '0.0000', '25.0000', '25.0000', '0.0000', '0.0000', '0.0000', '0.0000', 2, NULL, NULL, 'Arcadio Gym Short-32-Blue', NULL, 'Arcadio Gym Short-32-Blue', NULL, NULL, '25.0000', '0.0000', NULL, '0.0000', '25.0000', NULL, '25.0000', '25.0000', '25.0000', '25.0000', '0.0000', '0.0000', 0, NULL),
(7, NULL, 27, 31, '2016-04-29 08:15:46', '0000-00-00 00:00:00', NULL, NULL, NULL, '1.0000', '0.0000', '0.0000', '300.0000', '300.0000', '0.0000', '0.0000', '0.0000', '0.0000', 1, NULL, NULL, 'Ariel Roll Sleeve Sweatshirt', NULL, 'Ariel Roll Sleeve Sweatshirt', NULL, NULL, '150.0000', '0.0000', NULL, '0.0000', '150.0000', NULL, '150.0000', '150.0000', '300.0000', '300.0000', '0.0000', '0.0000', 0, NULL);

-- --------------------------------------------------------

--
-- Table structure for table `quote_id_mask`
--

CREATE TABLE `quote_id_mask` (
  `entity_id` int(10) UNSIGNED NOT NULL COMMENT 'Entity Id',
  `quote_id` int(10) UNSIGNED NOT NULL COMMENT 'Quote ID',
  `masked_id` varchar(32) DEFAULT NULL COMMENT 'Masked ID'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Quote ID and masked ID mapping';

--
-- Dumping data for table `quote_id_mask`
--

INSERT INTO `quote_id_mask` (`entity_id`, `quote_id`, `masked_id`) VALUES
(7, 7, '3c1a46d07f2115464ae130d311119281'),
(9, 9, '5bee4e94499f67f551e31e1c60ae1fb5'),
(1, 1, '63778bdc41af4c09e6df36116c8bebfb'),
(5, 5, '6c5b625ae1f6b322b1cae78c840f5195'),
(3, 3, '6fc24d9217343ff7d65c25f94ef82fa1'),
(11, 12, '74ee3b22ee6a22afd8f1b8408c5c009a'),
(6, 6, 'b13e98a17004348d4552c2ccc3719094'),
(8, 8, 'c58073e948a034bcc2642031e6636610'),
(10, 10, 'ced3ae0722bd1897aa8c0a252c393fec'),
(2, 2, 'f15cd5b9311a3d848dcdf12cc417cbf8'),
(4, 4, 'fcd3b699548ba0b538787ea5099390c4');

-- --------------------------------------------------------

--
-- Table structure for table `quote_item`
--

CREATE TABLE `quote_item` (
  `item_id` int(10) UNSIGNED NOT NULL COMMENT 'Item Id',
  `quote_id` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Quote Id',
  `created_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT 'Created At',
  `updated_at` timestamp NOT NULL DEFAULT '0000-00-00 00:00:00' ON UPDATE CURRENT_TIMESTAMP COMMENT 'Updated At',
  `product_id` int(10) UNSIGNED DEFAULT NULL COMMENT 'Product Id',
  `store_id` smallint(5) UNSIGNED DEFAULT NULL COMMENT 'Store Id',
  `parent_item_id` int(10) UNSIGNED DEFAULT NULL COMMENT 'Parent Item Id',
  `is_virtual` smallint(5) UNSIGNED DEFAULT NULL COMMENT 'Is Virtual',
  `sku` varchar(255) DEFAULT NULL COMMENT 'Sku',
  `name` varchar(255) DEFAULT NULL COMMENT 'Name',
  `description` text COMMENT 'Description',
  `applied_rule_ids` text COMMENT 'Applied Rule Ids',
  `additional_data` text COMMENT 'Additional Data',
  `is_qty_decimal` smallint(5) UNSIGNED DEFAULT NULL COMMENT 'Is Qty Decimal',
  `no_discount` smallint(5) UNSIGNED DEFAULT '0' COMMENT 'No Discount',
  `weight` decimal(12,4) DEFAULT '0.0000' COMMENT 'Weight',
  `qty` decimal(12,4) NOT NULL DEFAULT '0.0000' COMMENT 'Qty',
  `price` decimal(12,4) NOT NULL DEFAULT '0.0000' COMMENT 'Price',
  `base_price` decimal(12,4) NOT NULL DEFAULT '0.0000' COMMENT 'Base Price',
  `custom_price` decimal(12,4) DEFAULT NULL COMMENT 'Custom Price',
  `discount_percent` decimal(12,4) DEFAULT '0.0000' COMMENT 'Discount Percent',
  `discount_amount` decimal(12,4) DEFAULT '0.0000' COMMENT 'Discount Amount',
  `base_discount_amount` decimal(12,4) DEFAULT '0.0000' COMMENT 'Base Discount Amount',
  `tax_percent` decimal(12,4) DEFAULT '0.0000' COMMENT 'Tax Percent',
  `tax_amount` decimal(12,4) DEFAULT '0.0000' COMMENT 'Tax Amount',
  `base_tax_amount` decimal(12,4) DEFAULT '0.0000' COMMENT 'Base Tax Amount',
  `row_total` decimal(12,4) NOT NULL DEFAULT '0.0000' COMMENT 'Row Total',
  `base_row_total` decimal(12,4) NOT NULL DEFAULT '0.0000' COMMENT 'Base Row Total',
  `row_total_with_discount` decimal(12,4) DEFAULT '0.0000' COMMENT 'Row Total With Discount',
  `row_weight` decimal(12,4) DEFAULT '0.0000' COMMENT 'Row Weight',
  `product_type` varchar(255) DEFAULT NULL COMMENT 'Product Type',
  `base_tax_before_discount` decimal(12,4) DEFAULT NULL COMMENT 'Base Tax Before Discount',
  `tax_before_discount` decimal(12,4) DEFAULT NULL COMMENT 'Tax Before Discount',
  `original_custom_price` decimal(12,4) DEFAULT NULL COMMENT 'Original Custom Price',
  `redirect_url` varchar(255) DEFAULT NULL COMMENT 'Redirect Url',
  `base_cost` decimal(12,4) DEFAULT NULL COMMENT 'Base Cost',
  `price_incl_tax` decimal(12,4) DEFAULT NULL COMMENT 'Price Incl Tax',
  `base_price_incl_tax` decimal(12,4) DEFAULT NULL COMMENT 'Base Price Incl Tax',
  `row_total_incl_tax` decimal(12,4) DEFAULT NULL COMMENT 'Row Total Incl Tax',
  `base_row_total_incl_tax` decimal(12,4) DEFAULT NULL COMMENT 'Base Row Total Incl Tax',
  `discount_tax_compensation_amount` decimal(12,4) DEFAULT NULL COMMENT 'Discount Tax Compensation Amount',
  `base_discount_tax_compensation_amount` decimal(12,4) DEFAULT NULL COMMENT 'Base Discount Tax Compensation Amount',
  `free_shipping` smallint(6) DEFAULT NULL,
  `gift_message_id` int(11) DEFAULT NULL COMMENT 'Gift Message Id',
  `weee_tax_applied` text COMMENT 'Weee Tax Applied',
  `weee_tax_applied_amount` decimal(12,4) DEFAULT NULL COMMENT 'Weee Tax Applied Amount',
  `weee_tax_applied_row_amount` decimal(12,4) DEFAULT NULL COMMENT 'Weee Tax Applied Row Amount',
  `weee_tax_disposition` decimal(12,4) DEFAULT NULL COMMENT 'Weee Tax Disposition',
  `weee_tax_row_disposition` decimal(12,4) DEFAULT NULL COMMENT 'Weee Tax Row Disposition',
  `base_weee_tax_applied_amount` decimal(12,4) DEFAULT NULL COMMENT 'Base Weee Tax Applied Amount',
  `base_weee_tax_applied_row_amnt` decimal(12,4) DEFAULT NULL COMMENT 'Base Weee Tax Applied Row Amnt',
  `base_weee_tax_disposition` decimal(12,4) DEFAULT NULL COMMENT 'Base Weee Tax Disposition',
  `base_weee_tax_row_disposition` decimal(12,4) DEFAULT NULL COMMENT 'Base Weee Tax Row Disposition'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Sales Flat Quote Item';

--
-- Dumping data for table `quote_item`
--

INSERT INTO `quote_item` (`item_id`, `quote_id`, `created_at`, `updated_at`, `product_id`, `store_id`, `parent_item_id`, `is_virtual`, `sku`, `name`, `description`, `applied_rule_ids`, `additional_data`, `is_qty_decimal`, `no_discount`, `weight`, `qty`, `price`, `base_price`, `custom_price`, `discount_percent`, `discount_amount`, `base_discount_amount`, `tax_percent`, `tax_amount`, `base_tax_amount`, `row_total`, `base_row_total`, `row_total_with_discount`, `row_weight`, `product_type`, `base_tax_before_discount`, `tax_before_discount`, `original_custom_price`, `redirect_url`, `base_cost`, `price_incl_tax`, `base_price_incl_tax`, `row_total_incl_tax`, `base_row_total_incl_tax`, `discount_tax_compensation_amount`, `base_discount_tax_compensation_amount`, `free_shipping`, `gift_message_id`, `weee_tax_applied`, `weee_tax_applied_amount`, `weee_tax_applied_row_amount`, `weee_tax_disposition`, `weee_tax_row_disposition`, `base_weee_tax_applied_amount`, `base_weee_tax_applied_row_amnt`, `base_weee_tax_disposition`, `base_weee_tax_row_disposition`) VALUES
(1, 1, '2016-04-19 07:27:41', '0000-00-00 00:00:00', 5, 1, NULL, 1, 'product configuration magento-red', 'product configuration magento', NULL, NULL, NULL, 0, 0, NULL, '1.0000', '120.0000', '120.0000', NULL, '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '120.0000', '120.0000', '0.0000', '0.0000', 'configurable', NULL, NULL, NULL, NULL, NULL, '120.0000', '120.0000', '120.0000', '120.0000', '0.0000', '0.0000', 0, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL),
(2, 1, '2016-04-19 07:27:41', '0000-00-00 00:00:00', 8, 1, 1, 1, 'product configuration magento-red', 'product configuration magento-red', NULL, NULL, NULL, 0, 0, NULL, '1.0000', '0.0000', '0.0000', NULL, '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', 'virtual', NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, 0, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL),
(3, 2, '2016-04-19 09:16:27', '0000-00-00 00:00:00', 2, 1, NULL, 1, 'Arcadio Gym Short-32-Blue', 'Arcadio Gym Short-32-Blue', NULL, NULL, NULL, 0, 0, NULL, '1.0000', '25.0000', '25.0000', NULL, '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '25.0000', '25.0000', '0.0000', '0.0000', 'virtual', NULL, NULL, NULL, NULL, NULL, '25.0000', '25.0000', '25.0000', '25.0000', '0.0000', '0.0000', 0, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL),
(4, 3, '2016-04-20 08:49:35', '0000-00-00 00:00:00', 1, 1, NULL, 0, 'Ariel Roll Sleeve Sweatshirt', 'Ariel Roll Sleeve Sweatshirt', NULL, NULL, NULL, 0, 0, NULL, '1.0000', '150.0000', '150.0000', NULL, '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '150.0000', '150.0000', '0.0000', '0.0000', 'simple', NULL, NULL, NULL, NULL, NULL, '150.0000', '150.0000', '150.0000', '150.0000', '0.0000', '0.0000', 0, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL),
(5, 3, '2016-04-20 08:51:44', '0000-00-00 00:00:00', 2, 1, NULL, 1, 'Arcadio Gym Short-32-Blue', 'Arcadio Gym Short-32-Blue', NULL, NULL, NULL, 0, 0, NULL, '1.0000', '25.0000', '25.0000', NULL, '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '25.0000', '25.0000', '0.0000', '0.0000', 'virtual', NULL, NULL, NULL, NULL, NULL, '25.0000', '25.0000', '25.0000', '25.0000', '0.0000', '0.0000', 0, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL),
(6, 3, '2016-04-20 09:01:20', '0000-00-00 00:00:00', 5, 1, NULL, 1, 'product configuration magento-blue', 'product configuration magento', NULL, NULL, NULL, 0, 0, NULL, '1.0000', '120.0000', '120.0000', NULL, '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '120.0000', '120.0000', '0.0000', '0.0000', 'configurable', NULL, NULL, NULL, NULL, NULL, '120.0000', '120.0000', '120.0000', '120.0000', '0.0000', '0.0000', 0, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL),
(7, 3, '2016-04-20 09:01:20', '0000-00-00 00:00:00', 6, 1, 6, 1, 'product configuration magento-blue', 'product configuration magento-blue', NULL, NULL, NULL, 0, 0, NULL, '1.0000', '0.0000', '0.0000', NULL, '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', 'virtual', NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, 0, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL),
(8, 4, '2016-04-21 02:27:58', '0000-00-00 00:00:00', 5, 1, NULL, 1, 'product configuration magento-blue', 'product configuration magento', NULL, NULL, NULL, 0, 0, NULL, '1.0000', '120.0000', '120.0000', NULL, '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '120.0000', '120.0000', '0.0000', '0.0000', 'configurable', NULL, NULL, NULL, NULL, NULL, '120.0000', '120.0000', '120.0000', '120.0000', '0.0000', '0.0000', 0, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL),
(9, 4, '2016-04-21 02:27:58', '0000-00-00 00:00:00', 6, 1, 8, 1, 'product configuration magento-blue', 'product configuration magento-blue', NULL, NULL, NULL, 0, 0, NULL, '1.0000', '0.0000', '0.0000', NULL, '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', 'virtual', NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, 0, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL),
(10, 5, '2016-04-25 04:01:13', '2016-04-25 04:01:23', 12, 1, NULL, 0, ' Ariel Roll Sleeve Sweatshirt women', ' Ariel Roll Sleeve Sweatshirt women', NULL, NULL, NULL, 0, 0, NULL, '2.0000', '80.0000', '80.0000', NULL, '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '160.0000', '160.0000', '0.0000', '0.0000', 'simple', NULL, NULL, NULL, NULL, NULL, '80.0000', '80.0000', '160.0000', '160.0000', '0.0000', '0.0000', 0, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL),
(11, 5, '2016-04-25 04:01:25', '0000-00-00 00:00:00', 4, 1, NULL, 1, 'Arcadio Gym Short', 'Arcadio Gym Short', NULL, NULL, NULL, 0, 0, NULL, '1.0000', '24.0000', '24.0000', NULL, '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '24.0000', '24.0000', '0.0000', '0.0000', 'virtual', NULL, NULL, NULL, NULL, NULL, '24.0000', '24.0000', '24.0000', '24.0000', '0.0000', '0.0000', 0, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL),
(12, 6, '2016-04-25 07:20:48', '0000-00-00 00:00:00', 1, 1, NULL, 0, 'Ariel Roll Sleeve Sweatshirt', 'Ariel Roll Sleeve Sweatshirt', NULL, NULL, NULL, 0, 0, NULL, '1.0000', '150.0000', '150.0000', NULL, '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '150.0000', '150.0000', '0.0000', '0.0000', 'simple', NULL, NULL, NULL, NULL, NULL, '150.0000', '150.0000', '150.0000', '150.0000', '0.0000', '0.0000', 0, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL),
(13, 6, '2016-04-25 07:20:50', '0000-00-00 00:00:00', 2, 1, NULL, 1, 'Arcadio Gym Short-32-Blue', 'Arcadio Gym Short-32-Blue', NULL, NULL, NULL, 0, 0, NULL, '1.0000', '25.0000', '25.0000', NULL, '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '25.0000', '25.0000', '0.0000', '0.0000', 'virtual', NULL, NULL, NULL, NULL, NULL, '25.0000', '25.0000', '25.0000', '25.0000', '0.0000', '0.0000', 0, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL),
(14, 7, '2016-04-27 08:08:24', '0000-00-00 00:00:00', 9, 1, NULL, 1, 'Magento Bundle Product Type-product configuration magento-blue', 'Magento Bundle Product Type', NULL, NULL, NULL, 0, 0, '0.0000', '1.0000', '120.0000', '120.0000', NULL, '0.0000', '0.0000', '0.0000', NULL, '0.0000', '0.0000', '120.0000', '120.0000', '0.0000', '0.0000', 'bundle', NULL, NULL, NULL, NULL, NULL, '120.0000', '120.0000', '120.0000', '120.0000', NULL, NULL, 0, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL),
(15, 7, '2016-04-27 08:08:24', '0000-00-00 00:00:00', 6, 1, 14, 1, 'product configuration magento-blue', 'product configuration magento-blue', NULL, NULL, NULL, 0, 0, NULL, '1.0000', '120.0000', '120.0000', NULL, '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '120.0000', '120.0000', '0.0000', '0.0000', 'virtual', NULL, NULL, NULL, NULL, NULL, '120.0000', '120.0000', '120.0000', '120.0000', '0.0000', '0.0000', 0, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL),
(16, 8, '2016-04-27 08:11:20', '0000-00-00 00:00:00', 5, 1, NULL, 1, 'product configuration magento-blue', 'product configuration magento', NULL, NULL, NULL, 0, 0, NULL, '1.0000', '120.0000', '120.0000', NULL, '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '120.0000', '120.0000', '0.0000', '0.0000', 'configurable', NULL, NULL, NULL, NULL, NULL, '120.0000', '120.0000', '120.0000', '120.0000', '0.0000', '0.0000', 0, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL),
(17, 8, '2016-04-27 08:11:20', '0000-00-00 00:00:00', 6, 1, 16, 1, 'product configuration magento-blue', 'product configuration magento-blue', NULL, NULL, NULL, 0, 0, NULL, '1.0000', '0.0000', '0.0000', NULL, '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', 'virtual', NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, 0, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL),
(18, 9, '2016-04-27 08:13:46', '0000-00-00 00:00:00', 3, 1, NULL, 1, 'Atomic Endurance Running Tee', 'Atomic Endurance Running Tee', NULL, NULL, NULL, 0, 0, NULL, '1.0000', '25.0000', '25.0000', NULL, '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '25.0000', '25.0000', '0.0000', '0.0000', 'virtual', NULL, NULL, NULL, NULL, NULL, '25.0000', '25.0000', '25.0000', '25.0000', '0.0000', '0.0000', 0, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL),
(19, 9, '2016-04-27 08:13:46', '0000-00-00 00:00:00', 4, 1, NULL, 1, 'Arcadio Gym Short', 'Arcadio Gym Short', NULL, NULL, NULL, 0, 0, NULL, '1.0000', '24.0000', '24.0000', NULL, '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '24.0000', '24.0000', '0.0000', '0.0000', 'virtual', NULL, NULL, NULL, NULL, NULL, '24.0000', '24.0000', '24.0000', '24.0000', '0.0000', '0.0000', 0, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL),
(20, 10, '2016-04-27 09:56:29', '0000-00-00 00:00:00', 12, 1, NULL, 0, ' Ariel Roll Sleeve Sweatshirt women', ' Ariel Roll Sleeve Sweatshirt women', NULL, NULL, NULL, 0, 0, NULL, '1.0000', '80.0000', '80.0000', NULL, '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '80.0000', '80.0000', '0.0000', '0.0000', 'simple', NULL, NULL, NULL, NULL, NULL, '80.0000', '80.0000', '80.0000', '80.0000', '0.0000', '0.0000', 0, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL),
(21, 11, '2016-04-28 02:48:10', '0000-00-00 00:00:00', 3, 1, NULL, 1, 'Atomic Endurance Running Tee', 'Atomic Endurance Running Tee', NULL, NULL, NULL, 0, 0, NULL, '1.0000', '25.0000', '25.0000', NULL, '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '25.0000', '25.0000', '0.0000', '0.0000', 'virtual', NULL, NULL, NULL, NULL, NULL, '25.0000', '25.0000', '25.0000', '25.0000', '0.0000', '0.0000', 0, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL),
(22, 11, '2016-04-28 02:48:10', '0000-00-00 00:00:00', 4, 1, NULL, 1, 'Arcadio Gym Short', 'Arcadio Gym Short', NULL, NULL, NULL, 0, 0, NULL, '1.0000', '24.0000', '24.0000', NULL, '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '24.0000', '24.0000', '0.0000', '0.0000', 'virtual', NULL, NULL, NULL, NULL, NULL, '24.0000', '24.0000', '24.0000', '24.0000', '0.0000', '0.0000', 0, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL),
(23, 11, '2016-04-28 03:04:55', '0000-00-00 00:00:00', 5, 1, NULL, 1, 'product configuration magento-blue', 'product configuration magento', NULL, NULL, NULL, 0, 0, NULL, '1.0000', '120.0000', '120.0000', NULL, '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '120.0000', '120.0000', '0.0000', '0.0000', 'configurable', NULL, NULL, NULL, NULL, NULL, '120.0000', '120.0000', '120.0000', '120.0000', '0.0000', '0.0000', 0, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL),
(24, 11, '2016-04-28 03:04:55', '0000-00-00 00:00:00', 6, 1, 23, 1, 'product configuration magento-blue', 'product configuration magento-blue', NULL, NULL, NULL, 0, 0, NULL, '1.0000', '0.0000', '0.0000', NULL, '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', 'virtual', NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, 0, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL),
(25, 12, '2016-04-28 03:12:29', '2016-04-29 08:23:02', 1, 1, NULL, 0, 'Ariel Roll Sleeve Sweatshirt', 'Ariel Roll Sleeve Sweatshirt', NULL, NULL, NULL, 0, 0, NULL, '3.0000', '150.0000', '150.0000', NULL, '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '450.0000', '450.0000', '0.0000', '0.0000', 'simple', NULL, NULL, NULL, NULL, NULL, '150.0000', '150.0000', '450.0000', '450.0000', '0.0000', '0.0000', 0, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL),
(26, 12, '2016-04-28 03:12:42', '0000-00-00 00:00:00', 2, 1, NULL, 1, 'Arcadio Gym Short-32-Blue', 'Arcadio Gym Short-32-Blue', NULL, NULL, NULL, 0, 0, NULL, '1.0000', '25.0000', '25.0000', NULL, '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '25.0000', '25.0000', '0.0000', '0.0000', 'virtual', NULL, NULL, NULL, NULL, NULL, '25.0000', '25.0000', '25.0000', '25.0000', '0.0000', '0.0000', 0, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL),
(31, 12, '2016-04-29 07:58:32', '2016-04-29 08:10:41', 1, 1, NULL, 0, 'Ariel Roll Sleeve Sweatshirt', 'Ariel Roll Sleeve Sweatshirt', NULL, NULL, NULL, 0, 0, NULL, '2.0000', '150.0000', '150.0000', NULL, '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '300.0000', '300.0000', '0.0000', '0.0000', 'simple', NULL, NULL, NULL, NULL, NULL, '150.0000', '150.0000', '300.0000', '300.0000', '0.0000', '0.0000', 0, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL),
(32, 12, '2016-04-29 08:10:41', '0000-00-00 00:00:00', 4, 1, NULL, 1, 'Arcadio Gym Short', 'Arcadio Gym Short', NULL, NULL, NULL, 0, 0, NULL, '1.0000', '24.0000', '24.0000', NULL, '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '24.0000', '24.0000', '0.0000', '0.0000', 'virtual', NULL, NULL, NULL, NULL, NULL, '24.0000', '24.0000', '24.0000', '24.0000', '0.0000', '0.0000', 0, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL),
(33, 12, '2016-04-29 08:10:41', '0000-00-00 00:00:00', 3, 1, NULL, 1, 'Atomic Endurance Running Tee', 'Atomic Endurance Running Tee', NULL, NULL, NULL, 0, 0, NULL, '1.0000', '25.0000', '25.0000', NULL, '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '25.0000', '25.0000', '0.0000', '0.0000', 'virtual', NULL, NULL, NULL, NULL, NULL, '25.0000', '25.0000', '25.0000', '25.0000', '0.0000', '0.0000', 0, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL),
(34, 12, '2016-04-29 08:10:41', '0000-00-00 00:00:00', 2, 1, NULL, 1, 'Arcadio Gym Short-32-Blue', 'Arcadio Gym Short-32-Blue', NULL, NULL, NULL, 0, 0, NULL, '1.0000', '25.0000', '25.0000', NULL, '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '25.0000', '25.0000', '0.0000', '0.0000', 'virtual', NULL, NULL, NULL, NULL, NULL, '25.0000', '25.0000', '25.0000', '25.0000', '0.0000', '0.0000', 0, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL);

-- --------------------------------------------------------

--
-- Table structure for table `quote_item_option`
--

CREATE TABLE `quote_item_option` (
  `option_id` int(10) UNSIGNED NOT NULL COMMENT 'Option Id',
  `item_id` int(10) UNSIGNED NOT NULL COMMENT 'Item Id',
  `product_id` int(10) UNSIGNED NOT NULL COMMENT 'Product Id',
  `code` varchar(255) NOT NULL COMMENT 'Code',
  `value` text COMMENT 'Value'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Sales Flat Quote Item Option';

--
-- Dumping data for table `quote_item_option`
--

INSERT INTO `quote_item_option` (`option_id`, `item_id`, `product_id`, `code`, `value`) VALUES
(1, 1, 5, 'info_buyRequest', 'a:6:{s:4:"uenc";s:84:"aHR0cDovL2xvY2FsaG9zdC92ZXNfZmFzb255L3Byb2R1Y3QtY29uZmlndXJhdGlvbi1tYWdlbnRvLmh0bWw,";s:7:"product";s:1:"5";s:28:"selected_configurable_option";s:1:"8";s:15:"related_product";s:0:"";s:15:"super_attribute";a:1:{i:90;s:1:"6";}s:3:"qty";s:1:"1";}'),
(2, 1, 5, 'attributes', 'a:1:{i:90;s:1:"6";}'),
(3, 1, 8, 'product_qty_8', '1'),
(4, 1, 8, 'simple_product', '8'),
(5, 2, 8, 'info_buyRequest', 'a:6:{s:4:"uenc";s:84:"aHR0cDovL2xvY2FsaG9zdC92ZXNfZmFzb255L3Byb2R1Y3QtY29uZmlndXJhdGlvbi1tYWdlbnRvLmh0bWw,";s:7:"product";s:1:"5";s:28:"selected_configurable_option";s:1:"8";s:15:"related_product";s:0:"";s:15:"super_attribute";a:1:{i:90;s:1:"6";}s:3:"qty";s:1:"1";}'),
(6, 2, 8, 'parent_product_id', '5'),
(7, 3, 2, 'info_buyRequest', 'a:3:{s:4:"uenc";s:52:"aHR0cDovL2xvY2FsaG9zdC92ZXNfZmFzb255L3dvbWVuLmh0bWw,";s:7:"product";s:1:"2";s:3:"qty";i:1;}'),
(8, 4, 1, 'info_buyRequest', 'a:3:{s:4:"uenc";s:52:"aHR0cDovL2xvY2FsaG9zdC92ZXNfZmFzb255L3dvbWVuLmh0bWw,";s:7:"product";s:1:"1";s:3:"qty";i:1;}'),
(9, 5, 2, 'info_buyRequest', 'a:3:{s:4:"uenc";s:52:"aHR0cDovL2xvY2FsaG9zdC92ZXNfZmFzb255L3dvbWVuLmh0bWw,";s:7:"product";s:1:"2";s:3:"qty";i:1;}'),
(10, 6, 5, 'info_buyRequest', 'a:6:{s:4:"uenc";s:100:"aHR0cDovL2xvY2FsaG9zdC92ZXNfZmFzb255L3Byb2R1Y3QtY29uZmlndXJhdGlvbi1tYWdlbnRvLmh0bWw_b3B0aW9ucz1jYXJ0";s:7:"product";s:1:"5";s:28:"selected_configurable_option";s:1:"6";s:15:"related_product";s:0:"";s:15:"super_attribute";a:1:{i:90;s:1:"4";}s:3:"qty";s:1:"1";}'),
(11, 6, 5, 'attributes', 'a:1:{i:90;s:1:"4";}'),
(12, 6, 6, 'product_qty_6', '1'),
(13, 6, 6, 'simple_product', '6'),
(14, 7, 6, 'info_buyRequest', 'a:6:{s:4:"uenc";s:100:"aHR0cDovL2xvY2FsaG9zdC92ZXNfZmFzb255L3Byb2R1Y3QtY29uZmlndXJhdGlvbi1tYWdlbnRvLmh0bWw_b3B0aW9ucz1jYXJ0";s:7:"product";s:1:"5";s:28:"selected_configurable_option";s:1:"6";s:15:"related_product";s:0:"";s:15:"super_attribute";a:1:{i:90;s:1:"4";}s:3:"qty";s:1:"1";}'),
(15, 7, 6, 'parent_product_id', '5'),
(16, 8, 5, 'info_buyRequest', 'a:6:{s:4:"uenc";s:84:"aHR0cDovL2xvY2FsaG9zdC92ZXNfZmFzb255L3Byb2R1Y3QtY29uZmlndXJhdGlvbi1tYWdlbnRvLmh0bWw,";s:7:"product";s:1:"5";s:28:"selected_configurable_option";s:1:"6";s:15:"related_product";s:0:"";s:15:"super_attribute";a:1:{i:90;s:1:"4";}s:3:"qty";s:1:"1";}'),
(17, 8, 5, 'attributes', 'a:1:{i:90;s:1:"4";}'),
(18, 8, 6, 'product_qty_6', '1'),
(19, 8, 6, 'simple_product', '6'),
(20, 9, 6, 'info_buyRequest', 'a:6:{s:4:"uenc";s:84:"aHR0cDovL2xvY2FsaG9zdC92ZXNfZmFzb255L3Byb2R1Y3QtY29uZmlndXJhdGlvbi1tYWdlbnRvLmh0bWw,";s:7:"product";s:1:"5";s:28:"selected_configurable_option";s:1:"6";s:15:"related_product";s:0:"";s:15:"super_attribute";a:1:{i:90;s:1:"4";}s:3:"qty";s:1:"1";}'),
(21, 9, 6, 'parent_product_id', '5'),
(22, 10, 12, 'info_buyRequest', 'a:5:{s:4:"uenc";s:92:"aHR0cDovL2xvY2FsaG9zdC92ZXNfZmFzb255L2FyaWVsLXJvbGwtc2xlZXZlLXN3ZWF0c2hpcnQtd29tZW4uaHRtbA,,";s:7:"product";s:2:"12";s:28:"selected_configurable_option";s:0:"";s:15:"related_product";s:0:"";s:3:"qty";s:1:"1";}'),
(23, 11, 4, 'info_buyRequest', 'a:5:{s:4:"uenc";s:68:"aHR0cDovL2xvY2FsaG9zdC92ZXNfZmFzb255L2FyY2FkaW8tZ3ltLXNob3J0Lmh0bWw,";s:7:"product";s:1:"4";s:28:"selected_configurable_option";s:0:"";s:15:"related_product";s:0:"";s:3:"qty";s:1:"1";}'),
(24, 12, 1, 'info_buyRequest', 'a:3:{s:4:"uenc";s:80:"aHR0cDovL2xvY2FsaG9zdC92ZXNfZmFzb255L21lbnMuaHRtbD9wcm9kdWN0X2xpc3RfbW9kZT1saXN0";s:7:"product";s:1:"1";s:3:"qty";i:1;}'),
(25, 13, 2, 'info_buyRequest', 'a:3:{s:4:"uenc";s:80:"aHR0cDovL2xvY2FsaG9zdC92ZXNfZmFzb255L21lbnMuaHRtbD9wcm9kdWN0X2xpc3RfbW9kZT1saXN0";s:7:"product";s:1:"2";s:3:"qty";i:1;}'),
(26, 14, 9, 'info_buyRequest', 'a:6:{s:4:"uenc";s:80:"aHR0cDovL2xvY2FsaG9zdC92ZXNfZmFzb255L21hZ2VudG8tYnVuZGxlLXByb2R1Y3QtdHlwZS5odG1s";s:7:"product";s:1:"9";s:28:"selected_configurable_option";s:0:"";s:15:"related_product";s:0:"";s:13:"bundle_option";a:1:{i:1;a:1:{i:6;s:1:"2";}}s:3:"qty";s:1:"1";}'),
(27, 14, 6, 'selection_qty_2', '1'),
(28, 14, 6, 'product_qty_6', '1'),
(29, 14, 9, 'bundle_identity', '9_2_1'),
(30, 14, 9, 'bundle_option_ids', 'a:1:{i:0;i:1;}'),
(31, 14, 9, 'bundle_selection_ids', 'a:1:{i:0;s:1:"2";}'),
(32, 15, 6, 'selection_id', '2'),
(33, 15, 6, 'info_buyRequest', 'a:6:{s:4:"uenc";s:80:"aHR0cDovL2xvY2FsaG9zdC92ZXNfZmFzb255L21hZ2VudG8tYnVuZGxlLXByb2R1Y3QtdHlwZS5odG1s";s:7:"product";s:1:"9";s:28:"selected_configurable_option";s:0:"";s:15:"related_product";s:0:"";s:13:"bundle_option";a:1:{i:1;a:1:{i:6;s:1:"2";}}s:3:"qty";s:1:"1";}'),
(34, 15, 6, 'bundle_option_ids', 'a:1:{i:0;i:1;}'),
(35, 15, 6, 'bundle_selection_attributes', 'a:4:{s:5:"price";d:120;s:3:"qty";d:1;s:12:"option_label";s:18:"Custom option name";s:9:"option_id";s:1:"1";}'),
(36, 15, 6, 'bundle_identity', '9_2_1'),
(37, 16, 5, 'info_buyRequest', 'a:6:{s:4:"uenc";s:84:"aHR0cDovL2xvY2FsaG9zdC92ZXNfZmFzb255L3Byb2R1Y3QtY29uZmlndXJhdGlvbi1tYWdlbnRvLmh0bWw,";s:7:"product";s:1:"5";s:28:"selected_configurable_option";s:1:"6";s:15:"related_product";s:0:"";s:15:"super_attribute";a:1:{i:90;s:1:"4";}s:3:"qty";s:1:"1";}'),
(38, 16, 5, 'attributes', 'a:1:{i:90;s:1:"4";}'),
(39, 16, 6, 'product_qty_6', '1'),
(40, 16, 6, 'simple_product', '6'),
(41, 17, 6, 'info_buyRequest', 'a:6:{s:4:"uenc";s:84:"aHR0cDovL2xvY2FsaG9zdC92ZXNfZmFzb255L3Byb2R1Y3QtY29uZmlndXJhdGlvbi1tYWdlbnRvLmh0bWw,";s:7:"product";s:1:"5";s:28:"selected_configurable_option";s:1:"6";s:15:"related_product";s:0:"";s:15:"super_attribute";a:1:{i:90;s:1:"4";}s:3:"qty";s:1:"1";}'),
(42, 17, 6, 'parent_product_id', '5'),
(43, 18, 3, 'info_buyRequest', 'a:1:{s:20:"super_product_config";a:2:{s:12:"product_type";s:7:"grouped";s:10:"product_id";s:2:"10";}}'),
(44, 18, 10, 'product_type', 'grouped'),
(45, 19, 4, 'info_buyRequest', 'a:1:{s:20:"super_product_config";a:2:{s:12:"product_type";s:7:"grouped";s:10:"product_id";s:2:"10";}}'),
(46, 19, 10, 'product_type', 'grouped'),
(47, 20, 12, 'info_buyRequest', 'a:3:{s:4:"uenc";s:40:"aHR0cDovL2xvY2FsaG9zdC92ZXNfZmFzb255Lw,,";s:7:"product";s:2:"12";s:3:"qty";i:1;}'),
(48, 21, 3, 'info_buyRequest', 'a:1:{s:20:"super_product_config";a:2:{s:12:"product_type";s:7:"grouped";s:10:"product_id";s:2:"10";}}'),
(49, 21, 10, 'product_type', 'grouped'),
(50, 22, 4, 'info_buyRequest', 'a:1:{s:20:"super_product_config";a:2:{s:12:"product_type";s:7:"grouped";s:10:"product_id";s:2:"10";}}'),
(51, 22, 10, 'product_type', 'grouped'),
(52, 23, 5, 'info_buyRequest', 'a:6:{s:4:"uenc";s:100:"aHR0cDovL2xvY2FsaG9zdC92ZXNfZmFzb255L3Byb2R1Y3QtY29uZmlndXJhdGlvbi1tYWdlbnRvLmh0bWw_b3B0aW9ucz1jYXJ0";s:7:"product";s:1:"5";s:28:"selected_configurable_option";s:1:"6";s:15:"related_product";s:0:"";s:15:"super_attribute";a:1:{i:90;s:1:"4";}s:3:"qty";s:1:"1";}'),
(53, 23, 5, 'attributes', 'a:1:{i:90;s:1:"4";}'),
(54, 23, 6, 'product_qty_6', '1'),
(55, 23, 6, 'simple_product', '6'),
(56, 24, 6, 'info_buyRequest', 'a:6:{s:4:"uenc";s:100:"aHR0cDovL2xvY2FsaG9zdC92ZXNfZmFzb255L3Byb2R1Y3QtY29uZmlndXJhdGlvbi1tYWdlbnRvLmh0bWw_b3B0aW9ucz1jYXJ0";s:7:"product";s:1:"5";s:28:"selected_configurable_option";s:1:"6";s:15:"related_product";s:0:"";s:15:"super_attribute";a:1:{i:90;s:1:"4";}s:3:"qty";s:1:"1";}'),
(57, 24, 6, 'parent_product_id', '5'),
(58, 25, 1, 'info_buyRequest', 'a:3:{s:4:"uenc";s:52:"aHR0cDovL2xvY2FsaG9zdC92ZXNfZmFzb255L3dvbWVuLmh0bWw,";s:7:"product";s:1:"1";s:3:"qty";i:1;}'),
(59, 26, 2, 'info_buyRequest', 'a:3:{s:4:"uenc";s:52:"aHR0cDovL2xvY2FsaG9zdC92ZXNfZmFzb255L3dvbWVuLmh0bWw,";s:7:"product";s:1:"2";s:3:"qty";i:1;}'),
(64, 31, 1, 'info_buyRequest', 'a:5:{s:4:"uenc";s:84:"aHR0cDovL2xvY2FsaG9zdC92ZXNfZmFzb255L2FyaWVsLXJvbGwtc2xlZXZlLXN3ZWF0c2hpcnQuaHRtbA,,";s:7:"product";s:1:"1";s:28:"selected_configurable_option";s:0:"";s:15:"related_product";s:0:"";s:3:"qty";s:1:"1";}'),
(65, 32, 4, 'info_buyRequest', 'a:5:{s:4:"uenc";s:68:"aHR0cDovL2xvY2FsaG9zdC92ZXNfZmFzb255L2FyY2FkaW8tZ3ltLXNob3J0Lmh0bWw,";s:7:"product";s:1:"4";s:28:"selected_configurable_option";s:0:"";s:15:"related_product";s:5:"3,1,2";s:3:"qty";s:1:"1";}'),
(66, 33, 3, 'info_buyRequest', 'a:1:{s:3:"qty";i:1;}'),
(67, 34, 2, 'info_buyRequest', 'a:1:{s:3:"qty";i:1;}');

-- --------------------------------------------------------

--
-- Table structure for table `quote_payment`
--

CREATE TABLE `quote_payment` (
  `payment_id` int(10) UNSIGNED NOT NULL COMMENT 'Payment Id',
  `quote_id` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Quote Id',
  `created_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT 'Created At',
  `updated_at` timestamp NOT NULL DEFAULT '0000-00-00 00:00:00' ON UPDATE CURRENT_TIMESTAMP COMMENT 'Updated At',
  `method` varchar(255) DEFAULT NULL COMMENT 'Method',
  `cc_type` varchar(255) DEFAULT NULL COMMENT 'Cc Type',
  `cc_number_enc` varchar(255) DEFAULT NULL COMMENT 'Cc Number Enc',
  `cc_last_4` varchar(255) DEFAULT NULL COMMENT 'Cc Last 4',
  `cc_cid_enc` varchar(255) DEFAULT NULL COMMENT 'Cc Cid Enc',
  `cc_owner` varchar(255) DEFAULT NULL COMMENT 'Cc Owner',
  `cc_exp_month` varchar(255) DEFAULT NULL COMMENT 'Cc Exp Month',
  `cc_exp_year` smallint(5) UNSIGNED DEFAULT '0' COMMENT 'Cc Exp Year',
  `cc_ss_owner` varchar(255) DEFAULT NULL COMMENT 'Cc Ss Owner',
  `cc_ss_start_month` smallint(5) UNSIGNED DEFAULT '0' COMMENT 'Cc Ss Start Month',
  `cc_ss_start_year` smallint(5) UNSIGNED DEFAULT '0' COMMENT 'Cc Ss Start Year',
  `po_number` varchar(255) DEFAULT NULL COMMENT 'Po Number',
  `additional_data` text COMMENT 'Additional Data',
  `cc_ss_issue` varchar(255) DEFAULT NULL COMMENT 'Cc Ss Issue',
  `additional_information` text COMMENT 'Additional Information',
  `paypal_payer_id` varchar(255) DEFAULT NULL COMMENT 'Paypal Payer Id',
  `paypal_payer_status` varchar(255) DEFAULT NULL COMMENT 'Paypal Payer Status',
  `paypal_correlation_id` varchar(255) DEFAULT NULL COMMENT 'Paypal Correlation Id'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Sales Flat Quote Payment';

--
-- Dumping data for table `quote_payment`
--

INSERT INTO `quote_payment` (`payment_id`, `quote_id`, `created_at`, `updated_at`, `method`, `cc_type`, `cc_number_enc`, `cc_last_4`, `cc_cid_enc`, `cc_owner`, `cc_exp_month`, `cc_exp_year`, `cc_ss_owner`, `cc_ss_start_month`, `cc_ss_start_year`, `po_number`, `additional_data`, `cc_ss_issue`, `additional_information`, `paypal_payer_id`, `paypal_payer_status`, `paypal_correlation_id`) VALUES
(1, 7, '2016-04-27 08:10:31', '0000-00-00 00:00:00', 'checkmo', NULL, NULL, NULL, NULL, NULL, NULL, 0, NULL, 0, 0, NULL, NULL, NULL, NULL, NULL, NULL, NULL),
(2, 8, '2016-04-27 08:13:29', '0000-00-00 00:00:00', 'checkmo', NULL, NULL, NULL, NULL, NULL, NULL, 0, NULL, 0, 0, NULL, NULL, NULL, NULL, NULL, NULL, NULL),
(3, 9, '2016-04-27 08:15:53', '0000-00-00 00:00:00', 'checkmo', NULL, NULL, NULL, NULL, NULL, NULL, 0, NULL, 0, 0, NULL, NULL, NULL, NULL, NULL, NULL, NULL),
(4, 11, '2016-04-28 03:06:19', '0000-00-00 00:00:00', 'checkmo', NULL, NULL, NULL, NULL, NULL, NULL, 0, NULL, 0, 0, NULL, NULL, NULL, NULL, NULL, NULL, NULL);

-- --------------------------------------------------------

--
-- Table structure for table `quote_shipping_rate`
--

CREATE TABLE `quote_shipping_rate` (
  `rate_id` int(10) UNSIGNED NOT NULL COMMENT 'Rate Id',
  `address_id` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Address Id',
  `created_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT 'Created At',
  `updated_at` timestamp NOT NULL DEFAULT '0000-00-00 00:00:00' ON UPDATE CURRENT_TIMESTAMP COMMENT 'Updated At',
  `carrier` varchar(255) DEFAULT NULL COMMENT 'Carrier',
  `carrier_title` varchar(255) DEFAULT NULL COMMENT 'Carrier Title',
  `code` varchar(255) DEFAULT NULL COMMENT 'Code',
  `method` varchar(255) DEFAULT NULL COMMENT 'Method',
  `method_description` text COMMENT 'Method Description',
  `price` decimal(12,4) NOT NULL DEFAULT '0.0000' COMMENT 'Price',
  `error_message` text COMMENT 'Error Message',
  `method_title` text COMMENT 'Method Title'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Sales Flat Quote Shipping Rate';

--
-- Dumping data for table `quote_shipping_rate`
--

INSERT INTO `quote_shipping_rate` (`rate_id`, `address_id`, `created_at`, `updated_at`, `carrier`, `carrier_title`, `code`, `method`, `method_description`, `price`, `error_message`, `method_title`) VALUES
(3, 27, '2016-04-29 08:23:02', '0000-00-00 00:00:00', 'flatrate', 'Flat Rate', 'flatrate_flatrate', 'flatrate', NULL, '25.0000', NULL, 'Fixed');

-- --------------------------------------------------------

--
-- Table structure for table `rating`
--

CREATE TABLE `rating` (
  `rating_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Rating Id',
  `entity_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Entity Id',
  `rating_code` varchar(64) NOT NULL COMMENT 'Rating Code',
  `position` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Rating Position On Storefront',
  `is_active` smallint(6) NOT NULL DEFAULT '1' COMMENT 'Rating is active.'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Ratings';

--
-- Dumping data for table `rating`
--

INSERT INTO `rating` (`rating_id`, `entity_id`, `rating_code`, `position`, `is_active`) VALUES
(1, 1, 'Quality', 0, 1),
(2, 1, 'Value', 0, 1),
(3, 1, 'Price', 0, 1);

-- --------------------------------------------------------

--
-- Table structure for table `rating_entity`
--

CREATE TABLE `rating_entity` (
  `entity_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Entity Id',
  `entity_code` varchar(64) NOT NULL COMMENT 'Entity Code'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Rating entities';

--
-- Dumping data for table `rating_entity`
--

INSERT INTO `rating_entity` (`entity_id`, `entity_code`) VALUES
(1, 'product'),
(2, 'product_review'),
(3, 'review');

-- --------------------------------------------------------

--
-- Table structure for table `rating_option`
--

CREATE TABLE `rating_option` (
  `option_id` int(10) UNSIGNED NOT NULL COMMENT 'Rating Option Id',
  `rating_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Rating Id',
  `code` varchar(32) NOT NULL COMMENT 'Rating Option Code',
  `value` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Rating Option Value',
  `position` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Ration option position on Storefront'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Rating options';

--
-- Dumping data for table `rating_option`
--

INSERT INTO `rating_option` (`option_id`, `rating_id`, `code`, `value`, `position`) VALUES
(1, 1, '1', 1, 1),
(2, 1, '2', 2, 2),
(3, 1, '3', 3, 3),
(4, 1, '4', 4, 4),
(5, 1, '5', 5, 5),
(6, 2, '1', 1, 1),
(7, 2, '2', 2, 2),
(8, 2, '3', 3, 3),
(9, 2, '4', 4, 4),
(10, 2, '5', 5, 5),
(11, 3, '1', 1, 1),
(12, 3, '2', 2, 2),
(13, 3, '3', 3, 3),
(14, 3, '4', 4, 4),
(15, 3, '5', 5, 5);

-- --------------------------------------------------------

--
-- Table structure for table `rating_option_vote`
--

CREATE TABLE `rating_option_vote` (
  `vote_id` bigint(20) UNSIGNED NOT NULL COMMENT 'Vote id',
  `option_id` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Vote option id',
  `remote_ip` varchar(16) NOT NULL COMMENT 'Customer IP',
  `remote_ip_long` bigint(20) NOT NULL DEFAULT '0' COMMENT 'Customer IP converted to long integer format',
  `customer_id` int(10) UNSIGNED DEFAULT '0' COMMENT 'Customer Id',
  `entity_pk_value` bigint(20) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Product id',
  `rating_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Rating id',
  `review_id` bigint(20) UNSIGNED DEFAULT NULL COMMENT 'Review id',
  `percent` smallint(6) NOT NULL DEFAULT '0' COMMENT 'Percent amount',
  `value` smallint(6) NOT NULL DEFAULT '0' COMMENT 'Vote option value'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Rating option values';

--
-- Dumping data for table `rating_option_vote`
--

INSERT INTO `rating_option_vote` (`vote_id`, `option_id`, `remote_ip`, `remote_ip_long`, `customer_id`, `entity_pk_value`, `rating_id`, `review_id`, `percent`, `value`) VALUES
(1, 14, '::1', 0, NULL, 12, 3, 7, 80, 4),
(2, 10, '::1', 0, NULL, 12, 2, 7, 100, 5),
(3, 5, '::1', 0, NULL, 12, 1, 7, 100, 5),
(16, 14, '::1', 0, NULL, 12, 3, 2, 80, 4),
(17, 9, '::1', 0, NULL, 12, 2, 2, 80, 4),
(18, 5, '::1', 0, NULL, 12, 1, 2, 100, 5),
(19, 13, '::1', 0, NULL, 12, 3, 1, 60, 3),
(20, 10, '::1', 0, NULL, 12, 2, 1, 100, 5),
(21, 5, '::1', 0, NULL, 12, 1, 1, 100, 5),
(22, 15, '::1', 0, NULL, 3, 3, 8, 100, 5),
(23, 10, '::1', 0, NULL, 3, 2, 8, 100, 5),
(24, 5, '::1', 0, NULL, 3, 1, 8, 100, 5),
(25, 14, '::1', 0, NULL, 2, 3, 9, 80, 4),
(26, 10, '::1', 0, NULL, 2, 2, 9, 100, 5),
(27, 5, '::1', 0, NULL, 2, 1, 9, 100, 5),
(28, 14, '::1', 0, NULL, 1, 3, 10, 80, 4),
(29, 9, '::1', 0, NULL, 1, 2, 10, 80, 4),
(30, 5, '::1', 0, NULL, 1, 1, 10, 100, 5),
(31, 15, '::1', 0, NULL, 5, 3, 11, 100, 5),
(32, 10, '::1', 0, NULL, 5, 2, 11, 100, 5),
(33, 5, '::1', 0, NULL, 5, 1, 11, 100, 5),
(34, 13, '::1', 0, NULL, 9, 3, 12, 60, 3),
(35, 9, '::1', 0, NULL, 9, 2, 12, 80, 4),
(36, 5, '::1', 0, NULL, 9, 1, 12, 100, 5),
(37, 14, '::1', 0, NULL, 10, 3, 13, 80, 4),
(38, 10, '::1', 0, NULL, 10, 2, 13, 100, 5),
(39, 5, '::1', 0, NULL, 10, 1, 13, 100, 5);

-- --------------------------------------------------------

--
-- Table structure for table `rating_option_vote_aggregated`
--

CREATE TABLE `rating_option_vote_aggregated` (
  `primary_id` int(11) NOT NULL COMMENT 'Vote aggregation id',
  `rating_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Rating id',
  `entity_pk_value` bigint(20) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Product id',
  `vote_count` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Vote dty',
  `vote_value_sum` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'General vote sum',
  `percent` smallint(6) NOT NULL DEFAULT '0' COMMENT 'Vote percent',
  `percent_approved` smallint(6) DEFAULT '0' COMMENT 'Vote percent approved by admin',
  `store_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Store Id'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Rating vote aggregated';

--
-- Dumping data for table `rating_option_vote_aggregated`
--

INSERT INTO `rating_option_vote_aggregated` (`primary_id`, `rating_id`, `entity_pk_value`, `vote_count`, `vote_value_sum`, `percent`, `percent_approved`, `store_id`) VALUES
(1, 3, 12, 3, 11, 73, 73, 0),
(2, 3, 12, 3, 11, 73, 73, 1),
(3, 2, 12, 3, 14, 93, 93, 0),
(4, 2, 12, 3, 14, 93, 93, 1),
(5, 1, 12, 3, 15, 100, 100, 0),
(6, 1, 12, 3, 15, 100, 100, 1),
(7, 1, 12, 3, 15, 100, 100, 2),
(8, 2, 12, 3, 14, 93, 93, 2),
(9, 3, 12, 3, 11, 73, 73, 2),
(28, 3, 3, 1, 5, 100, 100, 0),
(29, 3, 3, 1, 5, 100, 100, 1),
(30, 2, 3, 1, 5, 100, 100, 0),
(31, 2, 3, 1, 5, 100, 100, 1),
(32, 1, 3, 1, 5, 100, 100, 0),
(33, 1, 3, 1, 5, 100, 100, 1),
(34, 3, 2, 1, 4, 80, 80, 0),
(35, 3, 2, 1, 4, 80, 80, 1),
(36, 2, 2, 1, 5, 100, 100, 0),
(37, 2, 2, 1, 5, 100, 100, 1),
(38, 1, 2, 1, 5, 100, 100, 0),
(39, 1, 2, 1, 5, 100, 100, 1),
(40, 3, 1, 1, 4, 80, 80, 0),
(41, 3, 1, 1, 4, 80, 80, 1),
(42, 2, 1, 1, 4, 80, 80, 0),
(43, 2, 1, 1, 4, 80, 80, 1),
(44, 1, 1, 1, 5, 100, 100, 0),
(45, 1, 1, 1, 5, 100, 100, 1),
(46, 1, 2, 1, 5, 100, 100, 2),
(47, 2, 2, 1, 5, 100, 100, 2),
(48, 3, 2, 1, 4, 80, 80, 2),
(49, 1, 3, 1, 5, 100, 100, 2),
(50, 2, 3, 1, 5, 100, 100, 2),
(51, 3, 3, 1, 5, 100, 100, 2),
(52, 1, 1, 1, 5, 100, 100, 2),
(53, 2, 1, 1, 4, 80, 80, 2),
(54, 3, 1, 1, 4, 80, 80, 2),
(55, 3, 5, 1, 5, 100, 100, 0),
(56, 3, 5, 1, 5, 100, 100, 1),
(57, 2, 5, 1, 5, 100, 100, 0),
(58, 2, 5, 1, 5, 100, 100, 1),
(59, 1, 5, 1, 5, 100, 100, 0),
(60, 1, 5, 1, 5, 100, 100, 1),
(61, 3, 9, 1, 3, 60, 60, 0),
(62, 3, 9, 1, 3, 60, 60, 1),
(63, 2, 9, 1, 4, 80, 80, 0),
(64, 2, 9, 1, 4, 80, 80, 1),
(65, 1, 9, 1, 5, 100, 100, 0),
(66, 1, 9, 1, 5, 100, 100, 1),
(67, 3, 10, 1, 4, 80, 80, 0),
(68, 3, 10, 1, 4, 80, 80, 1),
(69, 2, 10, 1, 5, 100, 100, 0),
(70, 2, 10, 1, 5, 100, 100, 1),
(71, 1, 10, 1, 5, 100, 100, 0),
(72, 1, 10, 1, 5, 100, 100, 1),
(73, 1, 5, 1, 5, 100, 100, 2),
(74, 2, 5, 1, 5, 100, 100, 2),
(75, 3, 5, 1, 5, 100, 100, 2),
(76, 1, 9, 1, 5, 100, 100, 2),
(77, 2, 9, 1, 4, 80, 80, 2),
(78, 3, 9, 1, 3, 60, 60, 2),
(79, 1, 10, 1, 5, 100, 100, 2),
(80, 2, 10, 1, 5, 100, 100, 2),
(81, 3, 10, 1, 4, 80, 80, 2);

-- --------------------------------------------------------

--
-- Table structure for table `rating_store`
--

CREATE TABLE `rating_store` (
  `rating_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Rating id',
  `store_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Store id'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Rating Store';

--
-- Dumping data for table `rating_store`
--

INSERT INTO `rating_store` (`rating_id`, `store_id`) VALUES
(1, 0),
(1, 1),
(1, 2),
(2, 0),
(2, 1),
(2, 2),
(3, 0),
(3, 1),
(3, 2);

-- --------------------------------------------------------

--
-- Table structure for table `rating_title`
--

CREATE TABLE `rating_title` (
  `rating_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Rating Id',
  `store_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Store Id',
  `value` varchar(255) NOT NULL COMMENT 'Rating Label'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Rating Title';

--
-- Dumping data for table `rating_title`
--

INSERT INTO `rating_title` (`rating_id`, `store_id`, `value`) VALUES
(1, 1, 'Quality'),
(1, 2, 'Quality'),
(2, 1, 'Value'),
(2, 2, 'Value'),
(3, 1, 'Price'),
(3, 2, 'Price');

-- --------------------------------------------------------

--
-- Table structure for table `reporting_counts`
--

CREATE TABLE `reporting_counts` (
  `entity_id` int(10) UNSIGNED NOT NULL COMMENT 'Entity Id',
  `type` varchar(255) DEFAULT NULL COMMENT 'Item Reported',
  `count` int(10) UNSIGNED DEFAULT NULL COMMENT 'Count Value',
  `updated_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP COMMENT 'Updated At'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Reporting for all count related events generated via the cron job';

-- --------------------------------------------------------

--
-- Table structure for table `reporting_module_status`
--

CREATE TABLE `reporting_module_status` (
  `entity_id` int(10) UNSIGNED NOT NULL COMMENT 'Module Id',
  `name` varchar(255) DEFAULT NULL COMMENT 'Module Name',
  `active` varchar(255) DEFAULT NULL COMMENT 'Module Active Status',
  `setup_version` varchar(255) DEFAULT NULL COMMENT 'Module Version',
  `state` varchar(255) DEFAULT NULL COMMENT 'Module State',
  `updated_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP COMMENT 'Updated At'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Module Status Table';

-- --------------------------------------------------------

--
-- Table structure for table `reporting_orders`
--

CREATE TABLE `reporting_orders` (
  `entity_id` int(10) UNSIGNED NOT NULL COMMENT 'Entity Id',
  `customer_id` int(10) UNSIGNED DEFAULT NULL COMMENT 'Customer Id',
  `total` decimal(20,2) DEFAULT NULL COMMENT 'Total From Store',
  `total_base` decimal(20,2) DEFAULT NULL COMMENT 'Total From Base Currency',
  `item_count` int(10) UNSIGNED NOT NULL COMMENT 'Line Item Count',
  `updated_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT 'Updated At'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Reporting for all orders';

-- --------------------------------------------------------

--
-- Table structure for table `reporting_system_updates`
--

CREATE TABLE `reporting_system_updates` (
  `entity_id` int(10) UNSIGNED NOT NULL COMMENT 'Entity Id',
  `type` varchar(255) DEFAULT NULL COMMENT 'Update Type',
  `action` varchar(255) DEFAULT NULL COMMENT 'Action Performed',
  `updated_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT 'Updated At'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Reporting for system updates';

-- --------------------------------------------------------

--
-- Table structure for table `reporting_users`
--

CREATE TABLE `reporting_users` (
  `entity_id` int(10) UNSIGNED NOT NULL COMMENT 'Entity Id',
  `type` varchar(255) DEFAULT NULL COMMENT 'User Type',
  `action` varchar(255) DEFAULT NULL COMMENT 'Action Performed',
  `updated_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT 'Updated At'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Reporting for user actions';

-- --------------------------------------------------------

--
-- Table structure for table `report_compared_product_index`
--

CREATE TABLE `report_compared_product_index` (
  `index_id` bigint(20) UNSIGNED NOT NULL COMMENT 'Index Id',
  `visitor_id` int(10) UNSIGNED DEFAULT NULL COMMENT 'Visitor Id',
  `customer_id` int(10) UNSIGNED DEFAULT NULL COMMENT 'Customer Id',
  `product_id` int(10) UNSIGNED NOT NULL COMMENT 'Product Id',
  `store_id` smallint(5) UNSIGNED DEFAULT NULL COMMENT 'Store Id',
  `added_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT 'Added At'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Reports Compared Product Index Table';

--
-- Dumping data for table `report_compared_product_index`
--

INSERT INTO `report_compared_product_index` (`index_id`, `visitor_id`, `customer_id`, `product_id`, `store_id`, `added_at`) VALUES
(1, 69, NULL, 5, NULL, '2016-04-20 06:44:47'),
(2, 69, NULL, 2, NULL, '2016-04-20 07:03:37'),
(3, 69, NULL, 1, NULL, '2016-04-20 07:03:58'),
(5, 69, NULL, 4, NULL, '2016-04-20 07:05:27'),
(6, 70, NULL, 2, NULL, '2016-04-20 07:35:46'),
(7, NULL, 2, 3, NULL, '2016-04-29 08:57:28'),
(8, NULL, 2, 1, NULL, '2016-04-29 08:58:47'),
(9, NULL, 2, 10, NULL, '2016-04-29 08:58:56');

-- --------------------------------------------------------

--
-- Table structure for table `report_event`
--

CREATE TABLE `report_event` (
  `event_id` bigint(20) UNSIGNED NOT NULL COMMENT 'Event Id',
  `logged_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT 'Logged At',
  `event_type_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Event Type Id',
  `object_id` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Object Id',
  `subject_id` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Subject Id',
  `subtype` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Subtype',
  `store_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Store Id'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Reports Event Table';

--
-- Dumping data for table `report_event`
--

INSERT INTO `report_event` (`event_id`, `logged_at`, `event_type_id`, `object_id`, `subject_id`, `subtype`, `store_id`) VALUES
(1, '2016-04-16 03:14:25', 1, 1, 26, 1, 1),
(2, '2016-04-16 03:15:49', 1, 1, 26, 1, 1),
(3, '2016-04-16 03:16:11', 1, 1, 26, 1, 1),
(4, '2016-04-16 03:17:23', 1, 1, 26, 1, 1),
(5, '2016-04-18 04:20:28', 1, 1, 33, 1, 1),
(6, '2016-04-18 09:57:32', 1, 1, 46, 1, 1),
(7, '2016-04-18 09:58:32', 1, 1, 46, 1, 1),
(8, '2016-04-18 09:59:08', 1, 1, 46, 1, 1),
(9, '2016-04-18 10:02:36', 1, 1, 45, 1, 1),
(10, '2016-04-18 10:15:11', 1, 1, 45, 1, 1),
(11, '2016-04-18 10:15:31', 1, 1, 45, 1, 1),
(12, '2016-04-18 10:17:40', 1, 1, 45, 1, 1),
(13, '2016-04-18 10:18:44', 1, 1, 45, 1, 1),
(14, '2016-04-18 10:19:35', 1, 1, 45, 1, 1),
(15, '2016-04-18 10:29:50', 1, 1, 45, 1, 1),
(16, '2016-04-18 10:32:05', 1, 1, 45, 1, 1),
(17, '2016-04-18 10:32:36', 1, 1, 47, 1, 1),
(18, '2016-04-18 10:32:36', 1, 1, 48, 1, 1),
(19, '2016-04-18 10:34:22', 1, 1, 48, 1, 1),
(20, '2016-04-19 01:42:37', 1, 1, 49, 1, 1),
(21, '2016-04-19 01:44:09', 1, 1, 49, 1, 1),
(22, '2016-04-19 01:45:15', 1, 1, 49, 1, 1),
(23, '2016-04-19 01:47:02', 1, 1, 49, 1, 1),
(24, '2016-04-19 01:47:22', 1, 1, 49, 1, 1),
(25, '2016-04-19 01:47:34', 1, 1, 49, 1, 1),
(26, '2016-04-19 01:48:05', 1, 1, 49, 1, 1),
(27, '2016-04-19 04:34:47', 1, 1, 52, 1, 1),
(28, '2016-04-19 04:34:48', 1, 1, 53, 1, 1),
(29, '2016-04-19 06:53:07', 1, 4, 55, 1, 1),
(30, '2016-04-19 06:54:46', 1, 4, 55, 1, 1),
(31, '2016-04-19 06:56:29', 1, 4, 55, 1, 1),
(32, '2016-04-19 06:58:27', 1, 4, 55, 1, 1),
(33, '2016-04-19 06:58:30', 1, 2, 55, 1, 1),
(34, '2016-04-19 06:58:32', 1, 2, 55, 1, 1),
(35, '2016-04-19 06:59:17', 1, 2, 55, 1, 1),
(36, '2016-04-19 06:59:19', 1, 2, 55, 1, 1),
(37, '2016-04-19 07:00:02', 1, 2, 55, 1, 1),
(38, '2016-04-19 07:00:08', 1, 2, 57, 1, 1),
(39, '2016-04-19 07:01:06', 1, 2, 57, 1, 1),
(40, '2016-04-19 07:01:09', 1, 2, 57, 1, 1),
(41, '2016-04-19 07:16:51', 1, 2, 55, 1, 1),
(42, '2016-04-19 07:17:19', 1, 2, 57, 1, 1),
(43, '2016-04-19 07:17:22', 1, 2, 57, 1, 1),
(44, '2016-04-19 07:17:25', 1, 2, 57, 1, 1),
(45, '2016-04-19 07:25:14', 1, 5, 57, 1, 1),
(46, '2016-04-19 07:26:38', 1, 5, 57, 1, 1),
(47, '2016-04-19 07:27:41', 4, 5, 57, 1, 1),
(48, '2016-04-19 07:29:15', 1, 5, 57, 1, 1),
(49, '2016-04-19 07:29:33', 1, 5, 57, 1, 1),
(50, '2016-04-19 07:29:35', 1, 5, 57, 1, 1),
(51, '2016-04-19 07:29:37', 1, 5, 57, 1, 1),
(52, '2016-04-19 07:29:40', 1, 5, 57, 1, 1),
(53, '2016-04-19 08:20:08', 1, 5, 58, 1, 1),
(54, '2016-04-19 08:24:55', 1, 5, 58, 1, 1),
(55, '2016-04-19 09:06:54', 1, 5, 58, 1, 1),
(56, '2016-04-19 09:08:47', 1, 5, 58, 1, 1),
(57, '2016-04-19 09:16:27', 4, 2, 62, 1, 1),
(58, '2016-04-20 03:58:03', 1, 5, 67, 1, 1),
(59, '2016-04-20 04:40:45', 1, 5, 68, 1, 1),
(60, '2016-04-20 04:55:16', 1, 5, 68, 1, 1),
(61, '2016-04-20 06:44:27', 1, 5, 69, 1, 1),
(62, '2016-04-20 06:44:47', 3, 5, 69, 1, 1),
(63, '2016-04-20 06:44:51', 1, 5, 69, 1, 1),
(64, '2016-04-20 06:48:47', 1, 5, 69, 1, 1),
(65, '2016-04-20 06:49:10', 1, 5, 69, 1, 1),
(66, '2016-04-20 07:03:37', 3, 2, 69, 1, 1),
(67, '2016-04-20 07:03:58', 3, 1, 69, 1, 1),
(68, '2016-04-20 07:04:00', 3, 2, 69, 1, 1),
(69, '2016-04-20 07:05:27', 3, 4, 69, 1, 1),
(70, '2016-04-20 07:35:46', 3, 2, 70, 1, 1),
(71, '2016-04-20 07:41:03', 3, 1, 69, 1, 1),
(72, '2016-04-20 08:49:35', 4, 1, 74, 1, 1),
(73, '2016-04-20 08:51:44', 4, 2, 74, 1, 1),
(74, '2016-04-20 09:00:59', 1, 5, 74, 1, 1),
(75, '2016-04-20 09:01:13', 1, 5, 75, 1, 1),
(76, '2016-04-20 09:01:20', 4, 5, 74, 1, 1),
(77, '2016-04-20 09:05:29', 1, 5, 74, 1, 1),
(78, '2016-04-20 09:08:03', 1, 5, 74, 1, 1),
(79, '2016-04-20 09:09:30', 1, 5, 74, 1, 1),
(80, '2016-04-20 09:15:58', 1, 5, 74, 1, 1),
(81, '2016-04-21 01:38:45', 1, 1, 78, 1, 1),
(82, '2016-04-21 01:41:56', 1, 1, 78, 1, 1),
(83, '2016-04-21 01:45:31', 1, 1, 78, 1, 1),
(84, '2016-04-21 01:50:23', 1, 1, 78, 1, 1),
(85, '2016-04-21 01:55:21', 1, 1, 78, 1, 1),
(86, '2016-04-21 01:56:04', 1, 1, 78, 1, 1),
(87, '2016-04-21 02:02:41', 1, 1, 78, 1, 1),
(88, '2016-04-21 02:13:19', 1, 4, 78, 1, 1),
(89, '2016-04-21 02:13:56', 1, 1, 78, 1, 1),
(90, '2016-04-21 02:16:17', 1, 2, 78, 1, 1),
(91, '2016-04-21 02:16:27', 1, 2, 78, 1, 1),
(92, '2016-04-21 02:18:01', 1, 1, 78, 1, 1),
(93, '2016-04-21 02:18:08', 1, 2, 78, 1, 1),
(94, '2016-04-21 02:18:30', 1, 1, 78, 1, 1),
(95, '2016-04-21 02:18:34', 1, 2, 78, 1, 1),
(96, '2016-04-21 02:19:57', 1, 2, 78, 1, 1),
(97, '2016-04-21 02:26:34', 1, 2, 78, 1, 1),
(98, '2016-04-21 02:26:44', 1, 1, 78, 1, 1),
(99, '2016-04-21 02:26:57', 1, 2, 78, 1, 1),
(100, '2016-04-21 02:27:06', 1, 3, 78, 1, 1),
(101, '2016-04-21 02:27:29', 1, 5, 78, 1, 1),
(102, '2016-04-21 02:27:58', 4, 5, 78, 1, 1),
(103, '2016-04-21 02:29:08', 1, 5, 78, 1, 1),
(104, '2016-04-21 02:40:34', 1, 3, 79, 1, 1),
(105, '2016-04-21 02:43:38', 1, 5, 79, 1, 1),
(106, '2016-04-21 02:43:45', 1, 3, 79, 1, 1),
(107, '2016-04-21 02:43:59', 1, 5, 79, 1, 1),
(108, '2016-04-21 03:41:03', 1, 5, 82, 1, 1),
(109, '2016-04-21 03:46:06', 1, 1, 83, 1, 1),
(110, '2016-04-21 04:58:28', 1, 3, 88, 1, 1),
(111, '2016-04-21 06:42:04', 1, 3, 89, 1, 1),
(112, '2016-04-21 06:42:12', 1, 5, 91, 1, 1),
(113, '2016-04-22 09:11:02', 1, 3, 99, 1, 1),
(114, '2016-04-25 02:12:29', 1, 4, 119, 1, 1),
(115, '2016-04-25 02:16:08', 1, 4, 119, 1, 1),
(116, '2016-04-25 02:16:10', 1, 4, 119, 1, 1),
(117, '2016-04-25 02:16:38', 1, 9, 119, 1, 1),
(118, '2016-04-25 02:19:51', 1, 9, 119, 1, 1),
(119, '2016-04-25 02:23:40', 1, 9, 119, 1, 1),
(120, '2016-04-25 02:23:50', 1, 9, 119, 1, 1),
(121, '2016-04-25 02:24:54', 1, 4, 119, 1, 1),
(122, '2016-04-25 02:24:58', 1, 9, 119, 1, 1),
(123, '2016-04-25 02:25:46', 1, 9, 119, 1, 1),
(124, '2016-04-25 02:27:42', 1, 9, 119, 1, 1),
(125, '2016-04-25 02:35:21', 1, 10, 119, 1, 1),
(126, '2016-04-25 02:36:04', 1, 10, 119, 1, 1),
(127, '2016-04-25 02:37:23', 1, 10, 119, 1, 1),
(128, '2016-04-25 02:43:24', 1, 10, 119, 1, 1),
(129, '2016-04-25 02:46:42', 1, 4, 119, 1, 1),
(130, '2016-04-25 02:59:14', 1, 12, 119, 1, 1),
(131, '2016-04-25 03:00:23', 1, 12, 119, 1, 1),
(132, '2016-04-25 03:00:59', 1, 9, 119, 1, 1),
(133, '2016-04-25 03:01:23', 1, 12, 119, 1, 1),
(134, '2016-04-25 03:36:50', 1, 12, 124, 1, 1),
(135, '2016-04-25 03:59:52', 1, 4, 124, 1, 1),
(136, '2016-04-25 04:00:08', 1, 12, 124, 1, 1),
(137, '2016-04-25 04:01:13', 4, 12, 124, 1, 1),
(138, '2016-04-25 04:01:25', 4, 4, 124, 1, 1),
(139, '2016-04-25 07:20:48', 4, 1, 127, 1, 1),
(140, '2016-04-25 07:20:50', 4, 2, 127, 1, 1),
(141, '2016-04-25 09:56:32', 1, 4, 128, 1, 1),
(142, '2016-04-25 10:13:32', 1, 4, 128, 1, 1),
(143, '2016-04-25 10:14:19', 1, 4, 128, 1, 1),
(144, '2016-04-25 10:14:36', 1, 4, 128, 1, 1),
(145, '2016-04-25 10:18:24', 1, 12, 128, 1, 1),
(146, '2016-04-25 10:20:11', 1, 12, 128, 1, 1),
(147, '2016-04-25 10:23:56', 1, 12, 128, 1, 1),
(148, '2016-04-25 10:26:22', 1, 12, 129, 1, 1),
(149, '2016-04-25 10:29:40', 1, 12, 129, 1, 1),
(150, '2016-04-25 10:30:11', 1, 12, 129, 1, 1),
(151, '2016-04-25 10:31:33', 1, 12, 129, 1, 1),
(152, '2016-04-25 10:34:08', 1, 12, 129, 1, 1),
(153, '2016-04-25 10:34:58', 1, 12, 129, 1, 1),
(154, '2016-04-27 01:50:02', 1, 12, 130, 1, 1),
(155, '2016-04-27 01:56:40', 1, 12, 130, 1, 1),
(156, '2016-04-27 02:00:06', 1, 12, 130, 1, 1),
(157, '2016-04-27 02:00:43', 1, 12, 130, 1, 1),
(158, '2016-04-27 02:01:09', 1, 12, 130, 1, 1),
(159, '2016-04-27 02:01:36', 1, 12, 130, 1, 1),
(160, '2016-04-27 02:04:56', 1, 12, 130, 1, 1),
(161, '2016-04-27 02:09:20', 1, 12, 130, 1, 1),
(162, '2016-04-27 02:10:29', 1, 12, 130, 1, 1),
(163, '2016-04-27 02:11:50', 1, 12, 130, 1, 1),
(164, '2016-04-27 02:15:25', 1, 12, 130, 1, 1),
(165, '2016-04-27 02:26:25', 1, 12, 130, 1, 1),
(166, '2016-04-27 02:26:27', 1, 12, 130, 1, 1),
(167, '2016-04-27 02:26:29', 1, 12, 130, 1, 1),
(168, '2016-04-27 02:35:38', 1, 12, 130, 1, 1),
(169, '2016-04-27 02:53:14', 1, 12, 131, 1, 1),
(170, '2016-04-27 02:55:09', 1, 12, 131, 1, 1),
(171, '2016-04-27 02:55:28', 1, 12, 131, 1, 1),
(172, '2016-04-27 02:55:56', 1, 12, 132, 1, 1),
(173, '2016-04-27 02:56:26', 1, 12, 132, 1, 1),
(174, '2016-04-27 02:57:16', 1, 12, 132, 1, 1),
(175, '2016-04-27 02:57:28', 1, 12, 132, 1, 1),
(176, '2016-04-27 02:58:01', 1, 12, 133, 1, 1),
(177, '2016-04-27 02:59:05', 1, 12, 132, 1, 1),
(178, '2016-04-27 03:01:59', 1, 12, 133, 1, 1),
(179, '2016-04-27 03:13:44', 1, 12, 134, 1, 1),
(180, '2016-04-27 03:37:19', 1, 12, 133, 1, 1),
(181, '2016-04-27 03:50:54', 1, 12, 133, 1, 1),
(182, '2016-04-27 04:23:49', 1, 12, 135, 1, 1),
(183, '2016-04-27 04:24:57', 1, 12, 135, 1, 1),
(184, '2016-04-27 04:25:04', 1, 5, 135, 1, 1),
(185, '2016-04-27 04:25:11', 1, 9, 135, 1, 1),
(186, '2016-04-27 04:25:24', 1, 12, 135, 1, 1),
(187, '2016-04-27 04:26:03', 1, 12, 135, 1, 1),
(188, '2016-04-27 04:27:02', 1, 5, 135, 1, 1),
(189, '2016-04-27 04:27:23', 1, 9, 135, 1, 1),
(190, '2016-04-27 04:27:35', 1, 12, 135, 1, 1),
(191, '2016-04-27 04:28:10', 1, 1, 135, 1, 1),
(192, '2016-04-27 04:28:22', 1, 4, 135, 1, 1),
(193, '2016-04-27 04:32:55', 1, 4, 135, 1, 1),
(194, '2016-04-27 04:35:59', 1, 4, 135, 1, 1),
(195, '2016-04-27 06:56:50', 1, 12, 138, 1, 1),
(196, '2016-04-27 07:29:32', 1, 12, 138, 1, 1),
(197, '2016-04-27 07:35:00', 1, 12, 138, 1, 1),
(198, '2016-04-27 07:35:51', 1, 9, 138, 1, 1),
(199, '2016-04-27 07:45:52', 1, 12, 139, 1, 1),
(200, '2016-04-27 07:45:52', 1, 12, 140, 1, 1),
(201, '2016-04-27 07:56:03', 1, 12, 140, 1, 1),
(202, '2016-04-27 07:57:11', 1, 12, 140, 1, 1),
(203, '2016-04-27 08:00:06', 1, 12, 140, 1, 1),
(204, '2016-04-27 08:00:14', 1, 12, 141, 1, 1),
(205, '2016-04-27 08:00:33', 1, 12, 140, 1, 1),
(206, '2016-04-27 08:01:05', 1, 3, 140, 1, 1),
(207, '2016-04-27 08:01:08', 1, 2, 140, 1, 1),
(208, '2016-04-27 08:01:11', 1, 1, 140, 1, 1),
(209, '2016-04-27 08:03:22', 1, 3, 140, 1, 1),
(210, '2016-04-27 08:03:34', 1, 2, 140, 1, 1),
(211, '2016-04-27 08:03:52', 1, 1, 140, 1, 1),
(212, '2016-04-27 08:04:19', 1, 12, 140, 1, 1),
(213, '2016-04-27 08:05:47', 1, 5, 140, 1, 1),
(214, '2016-04-27 08:05:50', 1, 9, 140, 1, 1),
(215, '2016-04-27 08:05:53', 1, 10, 140, 1, 1),
(216, '2016-04-27 08:05:57', 1, 5, 141, 1, 1),
(217, '2016-04-27 08:06:15', 1, 5, 140, 1, 1),
(218, '2016-04-27 08:06:31', 1, 9, 140, 1, 1),
(219, '2016-04-27 08:06:49', 1, 10, 140, 1, 1),
(220, '2016-04-27 08:07:01', 1, 3, 140, 1, 1),
(221, '2016-04-27 08:07:04', 1, 2, 140, 1, 1),
(222, '2016-04-27 08:08:17', 1, 9, 141, 1, 1),
(223, '2016-04-27 08:08:24', 4, 9, 140, 1, 1),
(224, '2016-04-27 08:11:20', 4, 5, 140, 1, 1),
(225, '2016-04-27 08:13:46', 4, 3, 140, 1, 1),
(226, '2016-04-27 08:13:46', 4, 4, 140, 1, 1),
(227, '2016-04-27 08:23:19', 1, 12, 140, 1, 1),
(228, '2016-04-27 09:56:29', 4, 12, 143, 1, 1),
(229, '2016-04-28 02:47:17', 1, 10, 2, 0, 1),
(230, '2016-04-28 02:48:10', 4, 3, 2, 0, 1),
(231, '2016-04-28 02:48:10', 4, 4, 2, 0, 1),
(232, '2016-04-28 03:04:41', 1, 5, 2, 0, 1),
(233, '2016-04-28 03:04:55', 4, 5, 2, 0, 1),
(234, '2016-04-28 03:12:29', 4, 1, 146, 1, 1),
(235, '2016-04-28 03:12:42', 4, 2, 146, 1, 1),
(236, '2016-04-29 03:59:49', 1, 1, 154, 1, 1),
(237, '2016-04-29 07:53:49', 1, 2, 158, 1, 1),
(238, '2016-04-29 07:53:53', 1, 1, 158, 1, 1),
(239, '2016-04-29 07:55:11', 1, 1, 158, 1, 1),
(240, '2016-04-29 07:55:58', 1, 3, 158, 1, 1),
(241, '2016-04-29 07:56:01', 1, 4, 158, 1, 1),
(242, '2016-04-29 07:56:09', 1, 9, 158, 1, 1),
(243, '2016-04-29 07:56:13', 1, 5, 158, 1, 1),
(244, '2016-04-29 07:56:17', 1, 12, 158, 1, 1),
(245, '2016-04-29 07:56:20', 1, 10, 158, 1, 1),
(246, '2016-04-29 07:58:32', 4, 1, 158, 1, 1),
(247, '2016-04-29 08:00:17', 1, 4, 158, 1, 1),
(248, '2016-04-29 08:09:07', 1, 4, 158, 1, 1),
(249, '2016-04-29 08:10:07', 1, 4, 158, 1, 1),
(250, '2016-04-29 08:10:41', 4, 4, 158, 1, 1),
(251, '2016-04-29 08:10:41', 4, 3, 158, 1, 1),
(252, '2016-04-29 08:10:41', 4, 2, 158, 1, 1),
(253, '2016-04-29 08:15:39', 4, 1, 2, 0, 1),
(254, '2016-04-29 08:15:39', 4, 4, 2, 0, 1),
(255, '2016-04-29 08:15:39', 4, 3, 2, 0, 1),
(256, '2016-04-29 08:15:39', 4, 2, 2, 0, 1),
(257, '2016-04-29 08:20:18', 1, 1, 2, 0, 1),
(258, '2016-04-29 08:20:30', 1, 1, 2, 0, 1),
(259, '2016-04-29 08:21:24', 1, 1, 2, 0, 1),
(260, '2016-04-29 08:21:39', 1, 1, 2, 0, 1),
(261, '2016-04-29 08:28:36', 1, 1, 2, 0, 1),
(262, '2016-04-29 08:28:59', 1, 1, 2, 0, 1),
(263, '2016-04-29 08:29:14', 1, 1, 159, 1, 1),
(264, '2016-04-29 08:37:31', 1, 1, 159, 1, 1),
(265, '2016-04-29 08:48:29', 1, 1, 159, 1, 1),
(266, '2016-04-29 08:48:32', 1, 1, 159, 1, 1),
(267, '2016-04-29 08:57:28', 3, 3, 2, 0, 1),
(268, '2016-04-29 08:58:47', 3, 1, 2, 0, 1),
(269, '2016-04-29 08:58:53', 1, 1, 2, 0, 1),
(270, '2016-04-29 08:58:56', 3, 10, 2, 0, 1);

-- --------------------------------------------------------

--
-- Table structure for table `report_event_types`
--

CREATE TABLE `report_event_types` (
  `event_type_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Event Type Id',
  `event_name` varchar(64) NOT NULL COMMENT 'Event Name',
  `customer_login` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Customer Login'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Reports Event Type Table';

--
-- Dumping data for table `report_event_types`
--

INSERT INTO `report_event_types` (`event_type_id`, `event_name`, `customer_login`) VALUES
(1, 'catalog_product_view', 0),
(2, 'sendfriend_product', 0),
(3, 'catalog_product_compare_add_product', 0),
(4, 'checkout_cart_add_product', 0),
(5, 'wishlist_add_product', 0),
(6, 'wishlist_share', 0);

-- --------------------------------------------------------

--
-- Table structure for table `report_viewed_product_aggregated_daily`
--

CREATE TABLE `report_viewed_product_aggregated_daily` (
  `id` int(10) UNSIGNED NOT NULL COMMENT 'Id',
  `period` date DEFAULT NULL COMMENT 'Period',
  `store_id` smallint(5) UNSIGNED DEFAULT NULL COMMENT 'Store Id',
  `product_id` int(10) UNSIGNED DEFAULT NULL COMMENT 'Product Id',
  `product_name` varchar(255) DEFAULT NULL COMMENT 'Product Name',
  `product_price` decimal(12,4) NOT NULL DEFAULT '0.0000' COMMENT 'Product Price',
  `views_num` int(11) NOT NULL DEFAULT '0' COMMENT 'Number of Views',
  `rating_pos` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Rating Pos'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Most Viewed Products Aggregated Daily';

-- --------------------------------------------------------

--
-- Table structure for table `report_viewed_product_aggregated_monthly`
--

CREATE TABLE `report_viewed_product_aggregated_monthly` (
  `id` int(10) UNSIGNED NOT NULL COMMENT 'Id',
  `period` date DEFAULT NULL COMMENT 'Period',
  `store_id` smallint(5) UNSIGNED DEFAULT NULL COMMENT 'Store Id',
  `product_id` int(10) UNSIGNED DEFAULT NULL COMMENT 'Product Id',
  `product_name` varchar(255) DEFAULT NULL COMMENT 'Product Name',
  `product_price` decimal(12,4) NOT NULL DEFAULT '0.0000' COMMENT 'Product Price',
  `views_num` int(11) NOT NULL DEFAULT '0' COMMENT 'Number of Views',
  `rating_pos` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Rating Pos'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Most Viewed Products Aggregated Monthly';

-- --------------------------------------------------------

--
-- Table structure for table `report_viewed_product_aggregated_yearly`
--

CREATE TABLE `report_viewed_product_aggregated_yearly` (
  `id` int(10) UNSIGNED NOT NULL COMMENT 'Id',
  `period` date DEFAULT NULL COMMENT 'Period',
  `store_id` smallint(5) UNSIGNED DEFAULT NULL COMMENT 'Store Id',
  `product_id` int(10) UNSIGNED DEFAULT NULL COMMENT 'Product Id',
  `product_name` varchar(255) DEFAULT NULL COMMENT 'Product Name',
  `product_price` decimal(12,4) NOT NULL DEFAULT '0.0000' COMMENT 'Product Price',
  `views_num` int(11) NOT NULL DEFAULT '0' COMMENT 'Number of Views',
  `rating_pos` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Rating Pos'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Most Viewed Products Aggregated Yearly';

-- --------------------------------------------------------

--
-- Table structure for table `report_viewed_product_index`
--

CREATE TABLE `report_viewed_product_index` (
  `index_id` bigint(20) UNSIGNED NOT NULL COMMENT 'Index Id',
  `visitor_id` int(10) UNSIGNED DEFAULT NULL COMMENT 'Visitor Id',
  `customer_id` int(10) UNSIGNED DEFAULT NULL COMMENT 'Customer Id',
  `product_id` int(10) UNSIGNED NOT NULL COMMENT 'Product Id',
  `store_id` smallint(5) UNSIGNED DEFAULT NULL COMMENT 'Store Id',
  `added_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT 'Added At'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Reports Viewed Product Index Table';

--
-- Dumping data for table `report_viewed_product_index`
--

INSERT INTO `report_viewed_product_index` (`index_id`, `visitor_id`, `customer_id`, `product_id`, `store_id`, `added_at`) VALUES
(1, 26, NULL, 1, 1, '2016-04-16 03:14:25'),
(2, 33, NULL, 1, 1, '2016-04-18 04:20:27'),
(3, 46, NULL, 1, 1, '2016-04-18 09:57:32'),
(6, 45, NULL, 1, 1, '2016-04-18 10:02:36'),
(14, 47, NULL, 1, 1, '2016-04-18 10:32:36'),
(15, 48, NULL, 1, 1, '2016-04-18 10:32:36'),
(16, 49, NULL, 1, 1, '2016-04-19 01:42:36'),
(17, 52, NULL, 1, 1, '2016-04-19 04:34:47'),
(18, 53, NULL, 1, 1, '2016-04-19 04:34:48'),
(19, 55, NULL, 4, 1, '2016-04-19 06:53:07'),
(23, 55, NULL, 2, 1, '2016-04-19 06:58:29'),
(28, 57, NULL, 2, 1, '2016-04-19 07:00:08'),
(33, 57, NULL, 5, 1, '2016-04-19 07:25:14'),
(40, 58, NULL, 5, 1, '2016-04-19 08:20:08'),
(41, 67, NULL, 5, 1, '2016-04-20 03:58:03'),
(42, 68, NULL, 5, 1, '2016-04-20 04:40:45'),
(44, 69, NULL, 5, 1, '2016-04-20 06:44:27'),
(45, 74, NULL, 5, 1, '2016-04-20 09:00:59'),
(46, 75, NULL, 5, 1, '2016-04-20 09:01:13'),
(47, 78, NULL, 1, 1, '2016-04-21 01:38:45'),
(54, 78, NULL, 4, 1, '2016-04-21 02:13:18'),
(56, 78, NULL, 2, 1, '2016-04-21 02:16:17'),
(66, 78, NULL, 3, 1, '2016-04-21 02:27:06'),
(67, 78, NULL, 5, 1, '2016-04-21 02:27:29'),
(69, 79, NULL, 3, 1, '2016-04-21 02:40:34'),
(70, 79, NULL, 5, 1, '2016-04-21 02:43:38'),
(73, 82, NULL, 5, 1, '2016-04-21 03:41:03'),
(74, 83, NULL, 1, 1, '2016-04-21 03:46:06'),
(75, 88, NULL, 3, 1, '2016-04-21 04:58:27'),
(76, 89, NULL, 3, 1, '2016-04-21 06:42:04'),
(77, 91, NULL, 5, 1, '2016-04-21 06:42:12'),
(78, 99, NULL, 3, 1, '2016-04-22 09:11:02'),
(79, 119, NULL, 4, 1, '2016-04-25 02:12:29'),
(82, 119, NULL, 9, 1, '2016-04-25 02:16:38'),
(90, 119, NULL, 10, 1, '2016-04-25 02:35:21'),
(95, 119, NULL, 12, 1, '2016-04-25 02:59:14'),
(99, 124, NULL, 12, 1, '2016-04-25 03:36:50'),
(100, 124, NULL, 4, 1, '2016-04-25 03:59:52'),
(102, 128, NULL, 4, 1, '2016-04-25 09:56:32'),
(106, 128, NULL, 12, 1, '2016-04-25 10:18:24'),
(109, 129, NULL, 12, 1, '2016-04-25 10:26:22'),
(110, 130, NULL, 12, 1, '2016-04-27 01:50:02'),
(125, 131, NULL, 12, 1, '2016-04-27 02:53:14'),
(128, 132, NULL, 12, 1, '2016-04-27 02:55:56'),
(132, 133, NULL, 12, 1, '2016-04-27 02:58:01'),
(135, 134, NULL, 12, 1, '2016-04-27 03:13:44'),
(138, 135, NULL, 12, 1, '2016-04-27 04:23:49'),
(140, 135, NULL, 5, 1, '2016-04-27 04:25:04'),
(141, 135, NULL, 9, 1, '2016-04-27 04:25:11'),
(147, 135, NULL, 1, 1, '2016-04-27 04:28:10'),
(148, 135, NULL, 4, 1, '2016-04-27 04:28:22'),
(149, 138, NULL, 12, 1, '2016-04-27 06:56:50'),
(152, 138, NULL, 9, 1, '2016-04-27 07:35:51'),
(153, 139, NULL, 12, 1, '2016-04-27 07:45:51'),
(154, 140, NULL, 12, 1, '2016-04-27 07:45:52'),
(158, 141, NULL, 12, 1, '2016-04-27 08:00:14'),
(160, 140, NULL, 3, 1, '2016-04-27 08:01:05'),
(161, 140, NULL, 2, 1, '2016-04-27 08:01:08'),
(162, 140, NULL, 1, 1, '2016-04-27 08:01:10'),
(167, 140, NULL, 5, 1, '2016-04-27 08:05:47'),
(168, 140, NULL, 9, 1, '2016-04-27 08:05:50'),
(169, 140, NULL, 10, 1, '2016-04-27 08:05:53'),
(170, 141, NULL, 5, 1, '2016-04-27 08:05:57'),
(176, 141, NULL, 9, 1, '2016-04-27 08:08:17'),
(177, 158, 2, 10, 1, '2016-04-28 02:47:17'),
(178, 158, 2, 5, 1, '2016-04-28 03:04:41'),
(179, 154, NULL, 1, 1, '2016-04-29 03:59:49'),
(180, 158, 2, 2, 1, '2016-04-29 07:53:49'),
(181, 158, 2, 1, 1, '2016-04-29 07:53:53'),
(183, 158, 2, 3, 1, '2016-04-29 07:55:57'),
(184, 158, 2, 4, 1, '2016-04-29 07:56:01'),
(185, 158, 2, 9, 1, '2016-04-29 07:56:09'),
(187, 158, 2, 12, 1, '2016-04-29 07:56:17'),
(198, 159, NULL, 1, 1, '2016-04-29 08:29:14');

-- --------------------------------------------------------

--
-- Table structure for table `review`
--

CREATE TABLE `review` (
  `review_id` bigint(20) UNSIGNED NOT NULL COMMENT 'Review id',
  `created_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT 'Review create date',
  `entity_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Entity id',
  `entity_pk_value` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Product id',
  `status_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Status code'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Review base information';

--
-- Dumping data for table `review`
--

INSERT INTO `review` (`review_id`, `created_at`, `entity_id`, `entity_pk_value`, `status_id`) VALUES
(1, '2016-04-27 04:23:44', 1, 12, 1),
(2, '2016-04-27 04:24:52', 1, 12, 1),
(7, '2016-04-27 07:57:06', 1, 12, 1),
(8, '2016-04-27 08:03:17', 1, 3, 1),
(9, '2016-04-27 08:03:29', 1, 2, 1),
(10, '2016-04-27 08:03:47', 1, 1, 1),
(11, '2016-04-27 08:06:11', 1, 5, 1),
(12, '2016-04-27 08:06:27', 1, 9, 1),
(13, '2016-04-27 08:06:44', 1, 10, 1);

-- --------------------------------------------------------

--
-- Table structure for table `review_detail`
--

CREATE TABLE `review_detail` (
  `detail_id` bigint(20) UNSIGNED NOT NULL COMMENT 'Review detail id',
  `review_id` bigint(20) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Review id',
  `store_id` smallint(5) UNSIGNED DEFAULT '0' COMMENT 'Store id',
  `title` varchar(255) NOT NULL COMMENT 'Title',
  `detail` text NOT NULL COMMENT 'Detail description',
  `nickname` varchar(128) NOT NULL COMMENT 'User nickname',
  `customer_id` int(10) UNSIGNED DEFAULT NULL COMMENT 'Customer Id'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Review detail information';

--
-- Dumping data for table `review_detail`
--

INSERT INTO `review_detail` (`detail_id`, `review_id`, `store_id`, `title`, `detail`, `nickname`, `customer_id`) VALUES
(1, 1, 1, 'Venustheme demo', 'Since 2011 we try a lot of different templates and extensions and most of them was not worth the money they want for that. Support: nothing. Source code: bad written with a lot of mistakes. Customisation: hopefully in 100 years.\r\nThen we came across Venus Theme and Land of cooder. The templates was very easy to install, the support was great and not often to find at other companies for the double and more of the prices of the templates. They made all our customisations for our websites in a fast and easy way to an affordable price. And what was not to find as an extension: they wrote it perfectly so we have today three different webshops all build up with these amazing guys. We save a lot of time and money in the daily work now and if we need anything or one of our mates: they are the first way.', 'Le Lieu', NULL),
(2, 2, 1, 'All set. Works fine. ', 'Thank you for areagirovanie quick and patience with me.\r\nI am very glad that he had purchased the theme Made in you.', 'Le Lieu', NULL),
(7, 7, 1, 'Venustheme demo ', 'Also, this magento 2.0 theme is fully translated to 26 different kind of languages. You can configure and setup multiple languages and currencies for different store views.', 'Le Lieu', NULL),
(8, 8, 1, 'Venustheme demo ', 'Since 2011 we try a lot of different templates and extensions and most of them was not worth the money they want for that. Support: nothing. Source code: bad written with a lot of mistakes. Customisation: hopefully in 100 years.\r\nThen we came across Venus Theme and Land of cooder. The templates was very easy to install, the support was great and not often to find at other companies for the double and more of the prices of the templates. They made all our customisations for our websites in a fast and easy way to an affordable price. And what was not to find as an extension: they wrote it perfectly so we have today three different webshops all build up with these amazing guys. We save a lot of time and money in the daily work now and if we need anything or one of our mates: they are the first way. ', 'Le Lieu', NULL),
(9, 9, 1, 'Venustheme test', 'Since 2011 we try a lot of different templates and extensions and most of them was not worth the money they want for that. Support: nothing. Source code: bad written with a lot of mistakes. Customisation: hopefully in 100 years.\r\nThen we came across Venus Theme and Land of cooder. The templates was very easy to install, the support was great and not often to find at other companies for the double and more of the prices of the templates. They made all our customisations for our websites in a fast and easy way to an affordable price. And what was not to find as an extension: they wrote it perfectly so we have today three different webshops all build up with these amazing guys. We save a lot of time and money in the daily work now and if we need anything or one of our mates: they are the first way. ', 'Le Lieu', NULL),
(10, 10, 1, 'Venustheme test', 'Since 2011 we try a lot of different templates and extensions and most of them was not worth the money they want for that. Support: nothing. Source code: bad written with a lot of mistakes. Customisation: hopefully in 100 years.\r\nThen we came across Venus Theme and Land of cooder. The templates was very easy to install, the support was great and not often to find at other companies for the double and more of the prices of the templates. They made all our customisations for our websites in a fast and easy way to an affordable price. And what was not to find as an extension: they wrote it perfectly so we have today three different webshops all build up with these amazing guys. We save a lot of time and money in the daily work now and if we need anything or one of our mates: they are the first way. ', 'Le Lieu', NULL),
(11, 11, 1, 'Venustheme', 'Since 2011 we try a lot of different templates and extensions and most of them was not worth the money they want for that. Support: nothing. Source code: bad written with a lot of mistakes. Customisation: hopefully in 100 years.\r\nThen we came across Venus Theme and Land of cooder. The templates was very easy to install, the support was great and not often to find at other companies for the double and more of the prices of the templates. They made all our customisations for our websites in a fast and easy way to an affordable price. And what was not to find as an extension: they wrote it perfectly so we have today three different webshops all build up with these amazing guys. We save a lot of time and money in the daily work now and if we need anything or one of our mates: they are the first way. ', 'Le Lieu', NULL),
(12, 12, 1, 'Venustheme', 'Since 2011 we try a lot of different templates and extensions and most of them was not worth the money they want for that. Support: nothing. Source code: bad written with a lot of mistakes. Customisation: hopefully in 100 years.\r\nThen we came across Venus Theme and Land of cooder. The templates was very easy to install, the support was great and not often to find at other companies for the double and more of the prices of the templates. They made all our customisations for our websites in a fast and easy way to an affordable price. And what was not to find as an extension: they wrote it perfectly so we have today three different webshops all build up with these amazing guys. We save a lot of time and money in the daily work now and if we need anything or one of our mates: they are the first way. ', 'Le Lieu', NULL),
(13, 13, 1, 'Venustheme', 'Since 2011 we try a lot of different templates and extensions and most of them was not worth the money they want for that. Support: nothing. Source code: bad written with a lot of mistakes. Customisation: hopefully in 100 years.\r\nThen we came across Venus Theme and Land of cooder. The templates was very easy to install, the support was great and not often to find at other companies for the double and more of the prices of the templates. They made all our customisations for our websites in a fast and easy way to an affordable price. And what was not to find as an extension: they wrote it perfectly so we have today three different webshops all build up with these amazing guys. We save a lot of time and money in the daily work now and if we need anything or one of our mates: they are the first way. ', 'Le Lieu', NULL);

-- --------------------------------------------------------

--
-- Table structure for table `review_entity`
--

CREATE TABLE `review_entity` (
  `entity_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Review entity id',
  `entity_code` varchar(32) NOT NULL COMMENT 'Review entity code'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Review entities';

--
-- Dumping data for table `review_entity`
--

INSERT INTO `review_entity` (`entity_id`, `entity_code`) VALUES
(1, 'product'),
(2, 'customer'),
(3, 'category');

-- --------------------------------------------------------

--
-- Table structure for table `review_entity_summary`
--

CREATE TABLE `review_entity_summary` (
  `primary_id` bigint(20) NOT NULL COMMENT 'Summary review entity id',
  `entity_pk_value` bigint(20) NOT NULL DEFAULT '0' COMMENT 'Product id',
  `entity_type` smallint(6) NOT NULL DEFAULT '0' COMMENT 'Entity type id',
  `reviews_count` smallint(6) NOT NULL DEFAULT '0' COMMENT 'Qty of reviews',
  `rating_summary` smallint(6) NOT NULL DEFAULT '0' COMMENT 'Summarized rating',
  `store_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Store id'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Review aggregates';

--
-- Dumping data for table `review_entity_summary`
--

INSERT INTO `review_entity_summary` (`primary_id`, `entity_pk_value`, `entity_type`, `reviews_count`, `rating_summary`, `store_id`) VALUES
(1, 12, 1, 3, 89, 1),
(2, 12, 1, 3, 89, 2),
(3, 5, 1, 1, 100, 1),
(4, 5, 1, 1, 100, 2),
(5, 9, 1, 1, 80, 1),
(6, 9, 1, 1, 80, 2),
(7, 12, 1, 3, 89, 0),
(8, 9, 1, 1, 80, 0),
(9, 5, 1, 1, 100, 0),
(10, 3, 1, 1, 100, 1),
(11, 3, 1, 1, 100, 2),
(12, 2, 1, 1, 93, 1),
(13, 2, 1, 1, 93, 2),
(14, 1, 1, 1, 87, 1),
(15, 1, 1, 1, 87, 2),
(16, 2, 1, 1, 93, 0),
(17, 3, 1, 1, 100, 0),
(18, 1, 1, 1, 87, 0),
(19, 10, 1, 1, 93, 1),
(20, 10, 1, 1, 93, 2),
(21, 10, 1, 1, 93, 0);

-- --------------------------------------------------------

--
-- Table structure for table `review_status`
--

CREATE TABLE `review_status` (
  `status_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Status id',
  `status_code` varchar(32) NOT NULL COMMENT 'Status code'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Review statuses';

--
-- Dumping data for table `review_status`
--

INSERT INTO `review_status` (`status_id`, `status_code`) VALUES
(1, 'Approved'),
(2, 'Pending'),
(3, 'Not Approved');

-- --------------------------------------------------------

--
-- Table structure for table `review_store`
--

CREATE TABLE `review_store` (
  `review_id` bigint(20) UNSIGNED NOT NULL COMMENT 'Review Id',
  `store_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Store Id'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Review Store';

--
-- Dumping data for table `review_store`
--

INSERT INTO `review_store` (`review_id`, `store_id`) VALUES
(1, 0),
(1, 1),
(1, 2),
(2, 0),
(2, 1),
(2, 2),
(7, 0),
(7, 1),
(7, 2),
(8, 0),
(8, 1),
(8, 2),
(9, 0),
(9, 1),
(9, 2),
(10, 0),
(10, 1),
(10, 2),
(11, 0),
(11, 1),
(11, 2),
(12, 0),
(12, 1),
(12, 2),
(13, 0),
(13, 1),
(13, 2);

-- --------------------------------------------------------

--
-- Table structure for table `salesrule`
--

CREATE TABLE `salesrule` (
  `rule_id` int(10) UNSIGNED NOT NULL COMMENT 'Rule Id',
  `name` varchar(255) DEFAULT NULL COMMENT 'Name',
  `description` text COMMENT 'Description',
  `from_date` date DEFAULT NULL COMMENT 'From',
  `to_date` date DEFAULT NULL COMMENT 'To',
  `uses_per_customer` int(11) NOT NULL DEFAULT '0' COMMENT 'Uses Per Customer',
  `is_active` smallint(6) NOT NULL DEFAULT '0' COMMENT 'Is Active',
  `conditions_serialized` mediumtext COMMENT 'Conditions Serialized',
  `actions_serialized` mediumtext COMMENT 'Actions Serialized',
  `stop_rules_processing` smallint(6) NOT NULL DEFAULT '1' COMMENT 'Stop Rules Processing',
  `is_advanced` smallint(5) UNSIGNED NOT NULL DEFAULT '1' COMMENT 'Is Advanced',
  `product_ids` text COMMENT 'Product Ids',
  `sort_order` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Sort Order',
  `simple_action` varchar(32) DEFAULT NULL COMMENT 'Simple Action',
  `discount_amount` decimal(12,4) NOT NULL DEFAULT '0.0000' COMMENT 'Discount Amount',
  `discount_qty` decimal(12,4) DEFAULT NULL COMMENT 'Discount Qty',
  `discount_step` int(10) UNSIGNED NOT NULL COMMENT 'Discount Step',
  `apply_to_shipping` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Apply To Shipping',
  `times_used` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Times Used',
  `is_rss` smallint(6) NOT NULL DEFAULT '0' COMMENT 'Is Rss',
  `coupon_type` smallint(5) UNSIGNED NOT NULL DEFAULT '1' COMMENT 'Coupon Type',
  `use_auto_generation` smallint(6) NOT NULL DEFAULT '0' COMMENT 'Use Auto Generation',
  `uses_per_coupon` int(11) NOT NULL DEFAULT '0' COMMENT 'User Per Coupon',
  `simple_free_shipping` smallint(6) DEFAULT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Salesrule';

-- --------------------------------------------------------

--
-- Table structure for table `salesrule_coupon`
--

CREATE TABLE `salesrule_coupon` (
  `coupon_id` int(10) UNSIGNED NOT NULL COMMENT 'Coupon Id',
  `rule_id` int(10) UNSIGNED NOT NULL COMMENT 'Rule Id',
  `code` varchar(255) DEFAULT NULL COMMENT 'Code',
  `usage_limit` int(10) UNSIGNED DEFAULT NULL COMMENT 'Usage Limit',
  `usage_per_customer` int(10) UNSIGNED DEFAULT NULL COMMENT 'Usage Per Customer',
  `times_used` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Times Used',
  `expiration_date` timestamp NULL DEFAULT NULL COMMENT 'Expiration Date',
  `is_primary` smallint(5) UNSIGNED DEFAULT NULL COMMENT 'Is Primary',
  `created_at` timestamp NULL DEFAULT NULL COMMENT 'Coupon Code Creation Date',
  `type` smallint(6) DEFAULT '0' COMMENT 'Coupon Code Type'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Salesrule Coupon';

-- --------------------------------------------------------

--
-- Table structure for table `salesrule_coupon_aggregated`
--

CREATE TABLE `salesrule_coupon_aggregated` (
  `id` int(10) UNSIGNED NOT NULL COMMENT 'Id',
  `period` date NOT NULL COMMENT 'Period',
  `store_id` smallint(5) UNSIGNED DEFAULT NULL COMMENT 'Store Id',
  `order_status` varchar(50) DEFAULT NULL COMMENT 'Order Status',
  `coupon_code` varchar(50) DEFAULT NULL COMMENT 'Coupon Code',
  `coupon_uses` int(11) NOT NULL DEFAULT '0' COMMENT 'Coupon Uses',
  `subtotal_amount` decimal(12,4) NOT NULL DEFAULT '0.0000' COMMENT 'Subtotal Amount',
  `discount_amount` decimal(12,4) NOT NULL DEFAULT '0.0000' COMMENT 'Discount Amount',
  `total_amount` decimal(12,4) NOT NULL DEFAULT '0.0000' COMMENT 'Total Amount',
  `subtotal_amount_actual` decimal(12,4) NOT NULL DEFAULT '0.0000' COMMENT 'Subtotal Amount Actual',
  `discount_amount_actual` decimal(12,4) NOT NULL DEFAULT '0.0000' COMMENT 'Discount Amount Actual',
  `total_amount_actual` decimal(12,4) NOT NULL DEFAULT '0.0000' COMMENT 'Total Amount Actual',
  `rule_name` varchar(255) DEFAULT NULL COMMENT 'Rule Name'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Coupon Aggregated';

-- --------------------------------------------------------

--
-- Table structure for table `salesrule_coupon_aggregated_order`
--

CREATE TABLE `salesrule_coupon_aggregated_order` (
  `id` int(10) UNSIGNED NOT NULL COMMENT 'Id',
  `period` date NOT NULL COMMENT 'Period',
  `store_id` smallint(5) UNSIGNED DEFAULT NULL COMMENT 'Store Id',
  `order_status` varchar(50) DEFAULT NULL COMMENT 'Order Status',
  `coupon_code` varchar(50) DEFAULT NULL COMMENT 'Coupon Code',
  `coupon_uses` int(11) NOT NULL DEFAULT '0' COMMENT 'Coupon Uses',
  `subtotal_amount` decimal(12,4) NOT NULL DEFAULT '0.0000' COMMENT 'Subtotal Amount',
  `discount_amount` decimal(12,4) NOT NULL DEFAULT '0.0000' COMMENT 'Discount Amount',
  `total_amount` decimal(12,4) NOT NULL DEFAULT '0.0000' COMMENT 'Total Amount',
  `rule_name` varchar(255) DEFAULT NULL COMMENT 'Rule Name'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Coupon Aggregated Order';

-- --------------------------------------------------------

--
-- Table structure for table `salesrule_coupon_aggregated_updated`
--

CREATE TABLE `salesrule_coupon_aggregated_updated` (
  `id` int(10) UNSIGNED NOT NULL COMMENT 'Id',
  `period` date NOT NULL COMMENT 'Period',
  `store_id` smallint(5) UNSIGNED DEFAULT NULL COMMENT 'Store Id',
  `order_status` varchar(50) DEFAULT NULL COMMENT 'Order Status',
  `coupon_code` varchar(50) DEFAULT NULL COMMENT 'Coupon Code',
  `coupon_uses` int(11) NOT NULL DEFAULT '0' COMMENT 'Coupon Uses',
  `subtotal_amount` decimal(12,4) NOT NULL DEFAULT '0.0000' COMMENT 'Subtotal Amount',
  `discount_amount` decimal(12,4) NOT NULL DEFAULT '0.0000' COMMENT 'Discount Amount',
  `total_amount` decimal(12,4) NOT NULL DEFAULT '0.0000' COMMENT 'Total Amount',
  `subtotal_amount_actual` decimal(12,4) NOT NULL DEFAULT '0.0000' COMMENT 'Subtotal Amount Actual',
  `discount_amount_actual` decimal(12,4) NOT NULL DEFAULT '0.0000' COMMENT 'Discount Amount Actual',
  `total_amount_actual` decimal(12,4) NOT NULL DEFAULT '0.0000' COMMENT 'Total Amount Actual',
  `rule_name` varchar(255) DEFAULT NULL COMMENT 'Rule Name'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Salesrule Coupon Aggregated Updated';

-- --------------------------------------------------------

--
-- Table structure for table `salesrule_coupon_usage`
--

CREATE TABLE `salesrule_coupon_usage` (
  `coupon_id` int(10) UNSIGNED NOT NULL COMMENT 'Coupon Id',
  `customer_id` int(10) UNSIGNED NOT NULL COMMENT 'Customer Id',
  `times_used` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Times Used'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Salesrule Coupon Usage';

-- --------------------------------------------------------

--
-- Table structure for table `salesrule_customer`
--

CREATE TABLE `salesrule_customer` (
  `rule_customer_id` int(10) UNSIGNED NOT NULL COMMENT 'Rule Customer Id',
  `rule_id` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Rule Id',
  `customer_id` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Customer Id',
  `times_used` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Times Used'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Salesrule Customer';

-- --------------------------------------------------------

--
-- Table structure for table `salesrule_customer_group`
--

CREATE TABLE `salesrule_customer_group` (
  `rule_id` int(10) UNSIGNED NOT NULL COMMENT 'Rule Id',
  `customer_group_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Customer Group Id'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Sales Rules To Customer Groups Relations';

-- --------------------------------------------------------

--
-- Table structure for table `salesrule_label`
--

CREATE TABLE `salesrule_label` (
  `label_id` int(10) UNSIGNED NOT NULL COMMENT 'Label Id',
  `rule_id` int(10) UNSIGNED NOT NULL COMMENT 'Rule Id',
  `store_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Store Id',
  `label` varchar(255) DEFAULT NULL COMMENT 'Label'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Salesrule Label';

-- --------------------------------------------------------

--
-- Table structure for table `salesrule_product_attribute`
--

CREATE TABLE `salesrule_product_attribute` (
  `rule_id` int(10) UNSIGNED NOT NULL COMMENT 'Rule Id',
  `website_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Website Id',
  `customer_group_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Customer Group Id',
  `attribute_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Attribute Id'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Salesrule Product Attribute';

-- --------------------------------------------------------

--
-- Table structure for table `salesrule_website`
--

CREATE TABLE `salesrule_website` (
  `rule_id` int(10) UNSIGNED NOT NULL COMMENT 'Rule Id',
  `website_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Website Id'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Sales Rules To Websites Relations';

-- --------------------------------------------------------

--
-- Table structure for table `sales_bestsellers_aggregated_daily`
--

CREATE TABLE `sales_bestsellers_aggregated_daily` (
  `id` int(10) UNSIGNED NOT NULL COMMENT 'Id',
  `period` date DEFAULT NULL COMMENT 'Period',
  `store_id` smallint(5) UNSIGNED DEFAULT NULL COMMENT 'Store Id',
  `product_id` int(10) UNSIGNED DEFAULT NULL COMMENT 'Product Id',
  `product_name` varchar(255) DEFAULT NULL COMMENT 'Product Name',
  `product_price` decimal(12,4) NOT NULL DEFAULT '0.0000' COMMENT 'Product Price',
  `qty_ordered` decimal(12,4) NOT NULL DEFAULT '0.0000' COMMENT 'Qty Ordered',
  `rating_pos` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Rating Pos'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Sales Bestsellers Aggregated Daily';

-- --------------------------------------------------------

--
-- Table structure for table `sales_bestsellers_aggregated_monthly`
--

CREATE TABLE `sales_bestsellers_aggregated_monthly` (
  `id` int(10) UNSIGNED NOT NULL COMMENT 'Id',
  `period` date DEFAULT NULL COMMENT 'Period',
  `store_id` smallint(5) UNSIGNED DEFAULT NULL COMMENT 'Store Id',
  `product_id` int(10) UNSIGNED DEFAULT NULL COMMENT 'Product Id',
  `product_name` varchar(255) DEFAULT NULL COMMENT 'Product Name',
  `product_price` decimal(12,4) NOT NULL DEFAULT '0.0000' COMMENT 'Product Price',
  `qty_ordered` decimal(12,4) NOT NULL DEFAULT '0.0000' COMMENT 'Qty Ordered',
  `rating_pos` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Rating Pos'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Sales Bestsellers Aggregated Monthly';

-- --------------------------------------------------------

--
-- Table structure for table `sales_bestsellers_aggregated_yearly`
--

CREATE TABLE `sales_bestsellers_aggregated_yearly` (
  `id` int(10) UNSIGNED NOT NULL COMMENT 'Id',
  `period` date DEFAULT NULL COMMENT 'Period',
  `store_id` smallint(5) UNSIGNED DEFAULT NULL COMMENT 'Store Id',
  `product_id` int(10) UNSIGNED DEFAULT NULL COMMENT 'Product Id',
  `product_name` varchar(255) DEFAULT NULL COMMENT 'Product Name',
  `product_price` decimal(12,4) NOT NULL DEFAULT '0.0000' COMMENT 'Product Price',
  `qty_ordered` decimal(12,4) NOT NULL DEFAULT '0.0000' COMMENT 'Qty Ordered',
  `rating_pos` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Rating Pos'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Sales Bestsellers Aggregated Yearly';

-- --------------------------------------------------------

--
-- Table structure for table `sales_creditmemo`
--

CREATE TABLE `sales_creditmemo` (
  `entity_id` int(10) UNSIGNED NOT NULL COMMENT 'Entity Id',
  `store_id` smallint(5) UNSIGNED DEFAULT NULL COMMENT 'Store Id',
  `adjustment_positive` decimal(12,4) DEFAULT NULL COMMENT 'Adjustment Positive',
  `base_shipping_tax_amount` decimal(12,4) DEFAULT NULL COMMENT 'Base Shipping Tax Amount',
  `store_to_order_rate` decimal(12,4) DEFAULT NULL COMMENT 'Store To Order Rate',
  `base_discount_amount` decimal(12,4) DEFAULT NULL COMMENT 'Base Discount Amount',
  `base_to_order_rate` decimal(12,4) DEFAULT NULL COMMENT 'Base To Order Rate',
  `grand_total` decimal(12,4) DEFAULT NULL COMMENT 'Grand Total',
  `base_adjustment_negative` decimal(12,4) DEFAULT NULL COMMENT 'Base Adjustment Negative',
  `base_subtotal_incl_tax` decimal(12,4) DEFAULT NULL COMMENT 'Base Subtotal Incl Tax',
  `shipping_amount` decimal(12,4) DEFAULT NULL COMMENT 'Shipping Amount',
  `subtotal_incl_tax` decimal(12,4) DEFAULT NULL COMMENT 'Subtotal Incl Tax',
  `adjustment_negative` decimal(12,4) DEFAULT NULL COMMENT 'Adjustment Negative',
  `base_shipping_amount` decimal(12,4) DEFAULT NULL COMMENT 'Base Shipping Amount',
  `store_to_base_rate` decimal(12,4) DEFAULT NULL COMMENT 'Store To Base Rate',
  `base_to_global_rate` decimal(12,4) DEFAULT NULL COMMENT 'Base To Global Rate',
  `base_adjustment` decimal(12,4) DEFAULT NULL COMMENT 'Base Adjustment',
  `base_subtotal` decimal(12,4) DEFAULT NULL COMMENT 'Base Subtotal',
  `discount_amount` decimal(12,4) DEFAULT NULL COMMENT 'Discount Amount',
  `subtotal` decimal(12,4) DEFAULT NULL COMMENT 'Subtotal',
  `adjustment` decimal(12,4) DEFAULT NULL COMMENT 'Adjustment',
  `base_grand_total` decimal(12,4) DEFAULT NULL COMMENT 'Base Grand Total',
  `base_adjustment_positive` decimal(12,4) DEFAULT NULL COMMENT 'Base Adjustment Positive',
  `base_tax_amount` decimal(12,4) DEFAULT NULL COMMENT 'Base Tax Amount',
  `shipping_tax_amount` decimal(12,4) DEFAULT NULL COMMENT 'Shipping Tax Amount',
  `tax_amount` decimal(12,4) DEFAULT NULL COMMENT 'Tax Amount',
  `order_id` int(10) UNSIGNED NOT NULL COMMENT 'Order Id',
  `email_sent` smallint(5) UNSIGNED DEFAULT NULL COMMENT 'Email Sent',
  `send_email` smallint(5) UNSIGNED DEFAULT NULL COMMENT 'Send Email',
  `creditmemo_status` int(11) DEFAULT NULL COMMENT 'Creditmemo Status',
  `state` int(11) DEFAULT NULL COMMENT 'State',
  `shipping_address_id` int(11) DEFAULT NULL COMMENT 'Shipping Address Id',
  `billing_address_id` int(11) DEFAULT NULL COMMENT 'Billing Address Id',
  `invoice_id` int(11) DEFAULT NULL COMMENT 'Invoice Id',
  `store_currency_code` varchar(3) DEFAULT NULL COMMENT 'Store Currency Code',
  `order_currency_code` varchar(3) DEFAULT NULL COMMENT 'Order Currency Code',
  `base_currency_code` varchar(3) DEFAULT NULL COMMENT 'Base Currency Code',
  `global_currency_code` varchar(3) DEFAULT NULL COMMENT 'Global Currency Code',
  `transaction_id` varchar(255) DEFAULT NULL COMMENT 'Transaction Id',
  `increment_id` varchar(50) DEFAULT NULL COMMENT 'Increment Id',
  `created_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT 'Created At',
  `updated_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP COMMENT 'Updated At',
  `discount_tax_compensation_amount` decimal(12,4) DEFAULT NULL COMMENT 'Discount Tax Compensation Amount',
  `base_discount_tax_compensation_amount` decimal(12,4) DEFAULT NULL COMMENT 'Base Discount Tax Compensation Amount',
  `shipping_discount_tax_compensation_amount` decimal(12,4) DEFAULT NULL COMMENT 'Shipping Discount Tax Compensation Amount',
  `base_shipping_discount_tax_compensation_amnt` decimal(12,4) DEFAULT NULL COMMENT 'Base Shipping Discount Tax Compensation Amount',
  `shipping_incl_tax` decimal(12,4) DEFAULT NULL COMMENT 'Shipping Incl Tax',
  `base_shipping_incl_tax` decimal(12,4) DEFAULT NULL COMMENT 'Base Shipping Incl Tax',
  `discount_description` varchar(255) DEFAULT NULL COMMENT 'Discount Description',
  `customer_note` text COMMENT 'Customer Note',
  `customer_note_notify` smallint(5) UNSIGNED DEFAULT NULL COMMENT 'Customer Note Notify'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Sales Flat Creditmemo';

-- --------------------------------------------------------

--
-- Table structure for table `sales_creditmemo_comment`
--

CREATE TABLE `sales_creditmemo_comment` (
  `entity_id` int(10) UNSIGNED NOT NULL COMMENT 'Entity Id',
  `parent_id` int(10) UNSIGNED NOT NULL COMMENT 'Parent Id',
  `is_customer_notified` int(11) DEFAULT NULL COMMENT 'Is Customer Notified',
  `is_visible_on_front` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Is Visible On Front',
  `comment` text COMMENT 'Comment',
  `created_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT 'Created At'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Sales Flat Creditmemo Comment';

-- --------------------------------------------------------

--
-- Table structure for table `sales_creditmemo_grid`
--

CREATE TABLE `sales_creditmemo_grid` (
  `entity_id` int(10) UNSIGNED NOT NULL COMMENT 'Entity Id',
  `increment_id` varchar(50) DEFAULT NULL COMMENT 'Increment Id',
  `created_at` timestamp NULL DEFAULT NULL COMMENT 'Created At',
  `updated_at` timestamp NULL DEFAULT NULL COMMENT 'Updated At',
  `order_id` int(10) UNSIGNED NOT NULL COMMENT 'Order Id',
  `order_increment_id` varchar(50) DEFAULT NULL COMMENT 'Order Increment Id',
  `order_created_at` timestamp NULL DEFAULT NULL COMMENT 'Order Created At',
  `billing_name` varchar(255) DEFAULT NULL COMMENT 'Billing Name',
  `state` int(11) DEFAULT NULL COMMENT 'Status',
  `base_grand_total` decimal(12,4) DEFAULT NULL COMMENT 'Base Grand Total',
  `order_status` varchar(32) DEFAULT NULL COMMENT 'Order Status',
  `store_id` smallint(5) UNSIGNED DEFAULT NULL COMMENT 'Store Id',
  `billing_address` varchar(255) DEFAULT NULL COMMENT 'Billing Address',
  `shipping_address` varchar(255) DEFAULT NULL COMMENT 'Shipping Address',
  `customer_name` varchar(128) NOT NULL COMMENT 'Customer Name',
  `customer_email` varchar(128) DEFAULT NULL COMMENT 'Customer Email',
  `customer_group_id` smallint(6) DEFAULT NULL COMMENT 'Customer Group Id',
  `payment_method` varchar(32) DEFAULT NULL COMMENT 'Payment Method',
  `shipping_information` varchar(255) DEFAULT NULL COMMENT 'Shipping Method Name',
  `subtotal` decimal(12,4) DEFAULT NULL COMMENT 'Subtotal',
  `shipping_and_handling` decimal(12,4) DEFAULT NULL COMMENT 'Shipping and handling amount',
  `adjustment_positive` decimal(12,4) DEFAULT NULL COMMENT 'Adjustment Positive',
  `adjustment_negative` decimal(12,4) DEFAULT NULL COMMENT 'Adjustment Negative',
  `order_base_grand_total` decimal(12,4) DEFAULT NULL COMMENT 'Order Grand Total'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Sales Flat Creditmemo Grid';

-- --------------------------------------------------------

--
-- Table structure for table `sales_creditmemo_item`
--

CREATE TABLE `sales_creditmemo_item` (
  `entity_id` int(10) UNSIGNED NOT NULL COMMENT 'Entity Id',
  `parent_id` int(10) UNSIGNED NOT NULL COMMENT 'Parent Id',
  `base_price` decimal(12,4) DEFAULT NULL COMMENT 'Base Price',
  `tax_amount` decimal(12,4) DEFAULT NULL COMMENT 'Tax Amount',
  `base_row_total` decimal(12,4) DEFAULT NULL COMMENT 'Base Row Total',
  `discount_amount` decimal(12,4) DEFAULT NULL COMMENT 'Discount Amount',
  `row_total` decimal(12,4) DEFAULT NULL COMMENT 'Row Total',
  `base_discount_amount` decimal(12,4) DEFAULT NULL COMMENT 'Base Discount Amount',
  `price_incl_tax` decimal(12,4) DEFAULT NULL COMMENT 'Price Incl Tax',
  `base_tax_amount` decimal(12,4) DEFAULT NULL COMMENT 'Base Tax Amount',
  `base_price_incl_tax` decimal(12,4) DEFAULT NULL COMMENT 'Base Price Incl Tax',
  `qty` decimal(12,4) DEFAULT NULL COMMENT 'Qty',
  `base_cost` decimal(12,4) DEFAULT NULL COMMENT 'Base Cost',
  `price` decimal(12,4) DEFAULT NULL COMMENT 'Price',
  `base_row_total_incl_tax` decimal(12,4) DEFAULT NULL COMMENT 'Base Row Total Incl Tax',
  `row_total_incl_tax` decimal(12,4) DEFAULT NULL COMMENT 'Row Total Incl Tax',
  `product_id` int(11) DEFAULT NULL COMMENT 'Product Id',
  `order_item_id` int(11) DEFAULT NULL COMMENT 'Order Item Id',
  `additional_data` text COMMENT 'Additional Data',
  `description` text COMMENT 'Description',
  `sku` varchar(255) DEFAULT NULL COMMENT 'Sku',
  `name` varchar(255) DEFAULT NULL COMMENT 'Name',
  `discount_tax_compensation_amount` decimal(12,4) DEFAULT NULL COMMENT 'Discount Tax Compensation Amount',
  `base_discount_tax_compensation_amount` decimal(12,4) DEFAULT NULL COMMENT 'Base Discount Tax Compensation Amount',
  `tax_ratio` text COMMENT 'Ratio of tax in the creditmemo item over tax of the order item',
  `weee_tax_applied` text COMMENT 'Weee Tax Applied',
  `weee_tax_applied_amount` decimal(12,4) DEFAULT NULL COMMENT 'Weee Tax Applied Amount',
  `weee_tax_applied_row_amount` decimal(12,4) DEFAULT NULL COMMENT 'Weee Tax Applied Row Amount',
  `weee_tax_disposition` decimal(12,4) DEFAULT NULL COMMENT 'Weee Tax Disposition',
  `weee_tax_row_disposition` decimal(12,4) DEFAULT NULL COMMENT 'Weee Tax Row Disposition',
  `base_weee_tax_applied_amount` decimal(12,4) DEFAULT NULL COMMENT 'Base Weee Tax Applied Amount',
  `base_weee_tax_applied_row_amnt` decimal(12,4) DEFAULT NULL COMMENT 'Base Weee Tax Applied Row Amnt',
  `base_weee_tax_disposition` decimal(12,4) DEFAULT NULL COMMENT 'Base Weee Tax Disposition',
  `base_weee_tax_row_disposition` decimal(12,4) DEFAULT NULL COMMENT 'Base Weee Tax Row Disposition'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Sales Flat Creditmemo Item';

-- --------------------------------------------------------

--
-- Table structure for table `sales_invoice`
--

CREATE TABLE `sales_invoice` (
  `entity_id` int(10) UNSIGNED NOT NULL COMMENT 'Entity Id',
  `store_id` smallint(5) UNSIGNED DEFAULT NULL COMMENT 'Store Id',
  `base_grand_total` decimal(12,4) DEFAULT NULL COMMENT 'Base Grand Total',
  `shipping_tax_amount` decimal(12,4) DEFAULT NULL COMMENT 'Shipping Tax Amount',
  `tax_amount` decimal(12,4) DEFAULT NULL COMMENT 'Tax Amount',
  `base_tax_amount` decimal(12,4) DEFAULT NULL COMMENT 'Base Tax Amount',
  `store_to_order_rate` decimal(12,4) DEFAULT NULL COMMENT 'Store To Order Rate',
  `base_shipping_tax_amount` decimal(12,4) DEFAULT NULL COMMENT 'Base Shipping Tax Amount',
  `base_discount_amount` decimal(12,4) DEFAULT NULL COMMENT 'Base Discount Amount',
  `base_to_order_rate` decimal(12,4) DEFAULT NULL COMMENT 'Base To Order Rate',
  `grand_total` decimal(12,4) DEFAULT NULL COMMENT 'Grand Total',
  `shipping_amount` decimal(12,4) DEFAULT NULL COMMENT 'Shipping Amount',
  `subtotal_incl_tax` decimal(12,4) DEFAULT NULL COMMENT 'Subtotal Incl Tax',
  `base_subtotal_incl_tax` decimal(12,4) DEFAULT NULL COMMENT 'Base Subtotal Incl Tax',
  `store_to_base_rate` decimal(12,4) DEFAULT NULL COMMENT 'Store To Base Rate',
  `base_shipping_amount` decimal(12,4) DEFAULT NULL COMMENT 'Base Shipping Amount',
  `total_qty` decimal(12,4) DEFAULT NULL COMMENT 'Total Qty',
  `base_to_global_rate` decimal(12,4) DEFAULT NULL COMMENT 'Base To Global Rate',
  `subtotal` decimal(12,4) DEFAULT NULL COMMENT 'Subtotal',
  `base_subtotal` decimal(12,4) DEFAULT NULL COMMENT 'Base Subtotal',
  `discount_amount` decimal(12,4) DEFAULT NULL COMMENT 'Discount Amount',
  `billing_address_id` int(11) DEFAULT NULL COMMENT 'Billing Address Id',
  `is_used_for_refund` smallint(5) UNSIGNED DEFAULT NULL COMMENT 'Is Used For Refund',
  `order_id` int(10) UNSIGNED NOT NULL COMMENT 'Order Id',
  `email_sent` smallint(5) UNSIGNED DEFAULT NULL COMMENT 'Email Sent',
  `send_email` smallint(5) UNSIGNED DEFAULT NULL COMMENT 'Send Email',
  `can_void_flag` smallint(5) UNSIGNED DEFAULT NULL COMMENT 'Can Void Flag',
  `state` int(11) DEFAULT NULL COMMENT 'State',
  `shipping_address_id` int(11) DEFAULT NULL COMMENT 'Shipping Address Id',
  `store_currency_code` varchar(3) DEFAULT NULL COMMENT 'Store Currency Code',
  `transaction_id` varchar(255) DEFAULT NULL COMMENT 'Transaction Id',
  `order_currency_code` varchar(3) DEFAULT NULL COMMENT 'Order Currency Code',
  `base_currency_code` varchar(3) DEFAULT NULL COMMENT 'Base Currency Code',
  `global_currency_code` varchar(3) DEFAULT NULL COMMENT 'Global Currency Code',
  `increment_id` varchar(50) DEFAULT NULL COMMENT 'Increment Id',
  `created_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT 'Created At',
  `updated_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP COMMENT 'Updated At',
  `discount_tax_compensation_amount` decimal(12,4) DEFAULT NULL COMMENT 'Discount Tax Compensation Amount',
  `base_discount_tax_compensation_amount` decimal(12,4) DEFAULT NULL COMMENT 'Base Discount Tax Compensation Amount',
  `shipping_discount_tax_compensation_amount` decimal(12,4) DEFAULT NULL COMMENT 'Shipping Discount Tax Compensation Amount',
  `base_shipping_discount_tax_compensation_amnt` decimal(12,4) DEFAULT NULL COMMENT 'Base Shipping Discount Tax Compensation Amount',
  `shipping_incl_tax` decimal(12,4) DEFAULT NULL COMMENT 'Shipping Incl Tax',
  `base_shipping_incl_tax` decimal(12,4) DEFAULT NULL COMMENT 'Base Shipping Incl Tax',
  `base_total_refunded` decimal(12,4) DEFAULT NULL COMMENT 'Base Total Refunded',
  `discount_description` varchar(255) DEFAULT NULL COMMENT 'Discount Description',
  `customer_note` text COMMENT 'Customer Note',
  `customer_note_notify` smallint(5) UNSIGNED DEFAULT NULL COMMENT 'Customer Note Notify'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Sales Flat Invoice';

-- --------------------------------------------------------

--
-- Table structure for table `sales_invoiced_aggregated`
--

CREATE TABLE `sales_invoiced_aggregated` (
  `id` int(10) UNSIGNED NOT NULL COMMENT 'Id',
  `period` date DEFAULT NULL COMMENT 'Period',
  `store_id` smallint(5) UNSIGNED DEFAULT NULL COMMENT 'Store Id',
  `order_status` varchar(50) DEFAULT NULL COMMENT 'Order Status',
  `orders_count` int(11) NOT NULL DEFAULT '0' COMMENT 'Orders Count',
  `orders_invoiced` decimal(12,4) DEFAULT NULL COMMENT 'Orders Invoiced',
  `invoiced` decimal(12,4) DEFAULT NULL COMMENT 'Invoiced',
  `invoiced_captured` decimal(12,4) DEFAULT NULL COMMENT 'Invoiced Captured',
  `invoiced_not_captured` decimal(12,4) DEFAULT NULL COMMENT 'Invoiced Not Captured'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Sales Invoiced Aggregated';

-- --------------------------------------------------------

--
-- Table structure for table `sales_invoiced_aggregated_order`
--

CREATE TABLE `sales_invoiced_aggregated_order` (
  `id` int(10) UNSIGNED NOT NULL COMMENT 'Id',
  `period` date DEFAULT NULL COMMENT 'Period',
  `store_id` smallint(5) UNSIGNED DEFAULT NULL COMMENT 'Store Id',
  `order_status` varchar(50) NOT NULL COMMENT 'Order Status',
  `orders_count` int(11) NOT NULL DEFAULT '0' COMMENT 'Orders Count',
  `orders_invoiced` decimal(12,4) DEFAULT NULL COMMENT 'Orders Invoiced',
  `invoiced` decimal(12,4) DEFAULT NULL COMMENT 'Invoiced',
  `invoiced_captured` decimal(12,4) DEFAULT NULL COMMENT 'Invoiced Captured',
  `invoiced_not_captured` decimal(12,4) DEFAULT NULL COMMENT 'Invoiced Not Captured'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Sales Invoiced Aggregated Order';

-- --------------------------------------------------------

--
-- Table structure for table `sales_invoice_comment`
--

CREATE TABLE `sales_invoice_comment` (
  `entity_id` int(10) UNSIGNED NOT NULL COMMENT 'Entity Id',
  `parent_id` int(10) UNSIGNED NOT NULL COMMENT 'Parent Id',
  `is_customer_notified` smallint(5) UNSIGNED DEFAULT NULL COMMENT 'Is Customer Notified',
  `is_visible_on_front` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Is Visible On Front',
  `comment` text COMMENT 'Comment',
  `created_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT 'Created At'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Sales Flat Invoice Comment';

-- --------------------------------------------------------

--
-- Table structure for table `sales_invoice_grid`
--

CREATE TABLE `sales_invoice_grid` (
  `entity_id` int(10) UNSIGNED NOT NULL COMMENT 'Entity Id',
  `increment_id` varchar(50) DEFAULT NULL COMMENT 'Increment Id',
  `state` int(11) DEFAULT NULL COMMENT 'State',
  `store_id` smallint(5) UNSIGNED DEFAULT NULL COMMENT 'Store Id',
  `store_name` varchar(255) DEFAULT NULL COMMENT 'Store Name',
  `order_id` int(10) UNSIGNED NOT NULL COMMENT 'Order Id',
  `order_increment_id` varchar(50) DEFAULT NULL COMMENT 'Order Increment Id',
  `order_created_at` timestamp NULL DEFAULT NULL COMMENT 'Order Created At',
  `customer_name` varchar(255) DEFAULT NULL COMMENT 'Customer Name',
  `customer_email` varchar(255) DEFAULT NULL COMMENT 'Customer Email',
  `customer_group_id` smallint(6) DEFAULT NULL COMMENT 'Customer Group Id',
  `payment_method` varchar(128) DEFAULT NULL COMMENT 'Payment Method',
  `store_currency_code` varchar(3) DEFAULT NULL COMMENT 'Store Currency Code',
  `order_currency_code` varchar(3) DEFAULT NULL COMMENT 'Order Currency Code',
  `base_currency_code` varchar(3) DEFAULT NULL COMMENT 'Base Currency Code',
  `global_currency_code` varchar(3) DEFAULT NULL COMMENT 'Global Currency Code',
  `billing_name` varchar(255) DEFAULT NULL COMMENT 'Billing Name',
  `billing_address` varchar(255) DEFAULT NULL COMMENT 'Billing Address',
  `shipping_address` varchar(255) DEFAULT NULL COMMENT 'Shipping Address',
  `shipping_information` varchar(255) DEFAULT NULL COMMENT 'Shipping Method Name',
  `subtotal` decimal(12,4) DEFAULT NULL COMMENT 'Subtotal',
  `shipping_and_handling` decimal(12,4) DEFAULT NULL COMMENT 'Shipping and handling amount',
  `grand_total` decimal(12,4) DEFAULT NULL COMMENT 'Grand Total',
  `created_at` timestamp NULL DEFAULT NULL COMMENT 'Created At',
  `updated_at` timestamp NULL DEFAULT NULL COMMENT 'Updated At'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Sales Flat Invoice Grid';

-- --------------------------------------------------------

--
-- Table structure for table `sales_invoice_item`
--

CREATE TABLE `sales_invoice_item` (
  `entity_id` int(10) UNSIGNED NOT NULL COMMENT 'Entity Id',
  `parent_id` int(10) UNSIGNED NOT NULL COMMENT 'Parent Id',
  `base_price` decimal(12,4) DEFAULT NULL COMMENT 'Base Price',
  `tax_amount` decimal(12,4) DEFAULT NULL COMMENT 'Tax Amount',
  `base_row_total` decimal(12,4) DEFAULT NULL COMMENT 'Base Row Total',
  `discount_amount` decimal(12,4) DEFAULT NULL COMMENT 'Discount Amount',
  `row_total` decimal(12,4) DEFAULT NULL COMMENT 'Row Total',
  `base_discount_amount` decimal(12,4) DEFAULT NULL COMMENT 'Base Discount Amount',
  `price_incl_tax` decimal(12,4) DEFAULT NULL COMMENT 'Price Incl Tax',
  `base_tax_amount` decimal(12,4) DEFAULT NULL COMMENT 'Base Tax Amount',
  `base_price_incl_tax` decimal(12,4) DEFAULT NULL COMMENT 'Base Price Incl Tax',
  `qty` decimal(12,4) DEFAULT NULL COMMENT 'Qty',
  `base_cost` decimal(12,4) DEFAULT NULL COMMENT 'Base Cost',
  `price` decimal(12,4) DEFAULT NULL COMMENT 'Price',
  `base_row_total_incl_tax` decimal(12,4) DEFAULT NULL COMMENT 'Base Row Total Incl Tax',
  `row_total_incl_tax` decimal(12,4) DEFAULT NULL COMMENT 'Row Total Incl Tax',
  `product_id` int(11) DEFAULT NULL COMMENT 'Product Id',
  `order_item_id` int(11) DEFAULT NULL COMMENT 'Order Item Id',
  `additional_data` text COMMENT 'Additional Data',
  `description` text COMMENT 'Description',
  `sku` varchar(255) DEFAULT NULL COMMENT 'Sku',
  `name` varchar(255) DEFAULT NULL COMMENT 'Name',
  `discount_tax_compensation_amount` decimal(12,4) DEFAULT NULL COMMENT 'Discount Tax Compensation Amount',
  `base_discount_tax_compensation_amount` decimal(12,4) DEFAULT NULL COMMENT 'Base Discount Tax Compensation Amount',
  `tax_ratio` text COMMENT 'Ratio of tax invoiced over tax of the order item',
  `weee_tax_applied` text COMMENT 'Weee Tax Applied',
  `weee_tax_applied_amount` decimal(12,4) DEFAULT NULL COMMENT 'Weee Tax Applied Amount',
  `weee_tax_applied_row_amount` decimal(12,4) DEFAULT NULL COMMENT 'Weee Tax Applied Row Amount',
  `weee_tax_disposition` decimal(12,4) DEFAULT NULL COMMENT 'Weee Tax Disposition',
  `weee_tax_row_disposition` decimal(12,4) DEFAULT NULL COMMENT 'Weee Tax Row Disposition',
  `base_weee_tax_applied_amount` decimal(12,4) DEFAULT NULL COMMENT 'Base Weee Tax Applied Amount',
  `base_weee_tax_applied_row_amnt` decimal(12,4) DEFAULT NULL COMMENT 'Base Weee Tax Applied Row Amnt',
  `base_weee_tax_disposition` decimal(12,4) DEFAULT NULL COMMENT 'Base Weee Tax Disposition',
  `base_weee_tax_row_disposition` decimal(12,4) DEFAULT NULL COMMENT 'Base Weee Tax Row Disposition'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Sales Flat Invoice Item';

-- --------------------------------------------------------

--
-- Table structure for table `sales_order`
--

CREATE TABLE `sales_order` (
  `entity_id` int(10) UNSIGNED NOT NULL COMMENT 'Entity Id',
  `state` varchar(32) DEFAULT NULL COMMENT 'State',
  `status` varchar(32) DEFAULT NULL COMMENT 'Status',
  `coupon_code` varchar(255) DEFAULT NULL COMMENT 'Coupon Code',
  `protect_code` varchar(255) DEFAULT NULL COMMENT 'Protect Code',
  `shipping_description` varchar(255) DEFAULT NULL COMMENT 'Shipping Description',
  `is_virtual` smallint(5) UNSIGNED DEFAULT NULL COMMENT 'Is Virtual',
  `store_id` smallint(5) UNSIGNED DEFAULT NULL COMMENT 'Store Id',
  `customer_id` int(10) UNSIGNED DEFAULT NULL COMMENT 'Customer Id',
  `base_discount_amount` decimal(12,4) DEFAULT NULL COMMENT 'Base Discount Amount',
  `base_discount_canceled` decimal(12,4) DEFAULT NULL COMMENT 'Base Discount Canceled',
  `base_discount_invoiced` decimal(12,4) DEFAULT NULL COMMENT 'Base Discount Invoiced',
  `base_discount_refunded` decimal(12,4) DEFAULT NULL COMMENT 'Base Discount Refunded',
  `base_grand_total` decimal(12,4) DEFAULT NULL COMMENT 'Base Grand Total',
  `base_shipping_amount` decimal(12,4) DEFAULT NULL COMMENT 'Base Shipping Amount',
  `base_shipping_canceled` decimal(12,4) DEFAULT NULL COMMENT 'Base Shipping Canceled',
  `base_shipping_invoiced` decimal(12,4) DEFAULT NULL COMMENT 'Base Shipping Invoiced',
  `base_shipping_refunded` decimal(12,4) DEFAULT NULL COMMENT 'Base Shipping Refunded',
  `base_shipping_tax_amount` decimal(12,4) DEFAULT NULL COMMENT 'Base Shipping Tax Amount',
  `base_shipping_tax_refunded` decimal(12,4) DEFAULT NULL COMMENT 'Base Shipping Tax Refunded',
  `base_subtotal` decimal(12,4) DEFAULT NULL COMMENT 'Base Subtotal',
  `base_subtotal_canceled` decimal(12,4) DEFAULT NULL COMMENT 'Base Subtotal Canceled',
  `base_subtotal_invoiced` decimal(12,4) DEFAULT NULL COMMENT 'Base Subtotal Invoiced',
  `base_subtotal_refunded` decimal(12,4) DEFAULT NULL COMMENT 'Base Subtotal Refunded',
  `base_tax_amount` decimal(12,4) DEFAULT NULL COMMENT 'Base Tax Amount',
  `base_tax_canceled` decimal(12,4) DEFAULT NULL COMMENT 'Base Tax Canceled',
  `base_tax_invoiced` decimal(12,4) DEFAULT NULL COMMENT 'Base Tax Invoiced',
  `base_tax_refunded` decimal(12,4) DEFAULT NULL COMMENT 'Base Tax Refunded',
  `base_to_global_rate` decimal(12,4) DEFAULT NULL COMMENT 'Base To Global Rate',
  `base_to_order_rate` decimal(12,4) DEFAULT NULL COMMENT 'Base To Order Rate',
  `base_total_canceled` decimal(12,4) DEFAULT NULL COMMENT 'Base Total Canceled',
  `base_total_invoiced` decimal(12,4) DEFAULT NULL COMMENT 'Base Total Invoiced',
  `base_total_invoiced_cost` decimal(12,4) DEFAULT NULL COMMENT 'Base Total Invoiced Cost',
  `base_total_offline_refunded` decimal(12,4) DEFAULT NULL COMMENT 'Base Total Offline Refunded',
  `base_total_online_refunded` decimal(12,4) DEFAULT NULL COMMENT 'Base Total Online Refunded',
  `base_total_paid` decimal(12,4) DEFAULT NULL COMMENT 'Base Total Paid',
  `base_total_qty_ordered` decimal(12,4) DEFAULT NULL COMMENT 'Base Total Qty Ordered',
  `base_total_refunded` decimal(12,4) DEFAULT NULL COMMENT 'Base Total Refunded',
  `discount_amount` decimal(12,4) DEFAULT NULL COMMENT 'Discount Amount',
  `discount_canceled` decimal(12,4) DEFAULT NULL COMMENT 'Discount Canceled',
  `discount_invoiced` decimal(12,4) DEFAULT NULL COMMENT 'Discount Invoiced',
  `discount_refunded` decimal(12,4) DEFAULT NULL COMMENT 'Discount Refunded',
  `grand_total` decimal(12,4) DEFAULT NULL COMMENT 'Grand Total',
  `shipping_amount` decimal(12,4) DEFAULT NULL COMMENT 'Shipping Amount',
  `shipping_canceled` decimal(12,4) DEFAULT NULL COMMENT 'Shipping Canceled',
  `shipping_invoiced` decimal(12,4) DEFAULT NULL COMMENT 'Shipping Invoiced',
  `shipping_refunded` decimal(12,4) DEFAULT NULL COMMENT 'Shipping Refunded',
  `shipping_tax_amount` decimal(12,4) DEFAULT NULL COMMENT 'Shipping Tax Amount',
  `shipping_tax_refunded` decimal(12,4) DEFAULT NULL COMMENT 'Shipping Tax Refunded',
  `store_to_base_rate` decimal(12,4) DEFAULT NULL COMMENT 'Store To Base Rate',
  `store_to_order_rate` decimal(12,4) DEFAULT NULL COMMENT 'Store To Order Rate',
  `subtotal` decimal(12,4) DEFAULT NULL COMMENT 'Subtotal',
  `subtotal_canceled` decimal(12,4) DEFAULT NULL COMMENT 'Subtotal Canceled',
  `subtotal_invoiced` decimal(12,4) DEFAULT NULL COMMENT 'Subtotal Invoiced',
  `subtotal_refunded` decimal(12,4) DEFAULT NULL COMMENT 'Subtotal Refunded',
  `tax_amount` decimal(12,4) DEFAULT NULL COMMENT 'Tax Amount',
  `tax_canceled` decimal(12,4) DEFAULT NULL COMMENT 'Tax Canceled',
  `tax_invoiced` decimal(12,4) DEFAULT NULL COMMENT 'Tax Invoiced',
  `tax_refunded` decimal(12,4) DEFAULT NULL COMMENT 'Tax Refunded',
  `total_canceled` decimal(12,4) DEFAULT NULL COMMENT 'Total Canceled',
  `total_invoiced` decimal(12,4) DEFAULT NULL COMMENT 'Total Invoiced',
  `total_offline_refunded` decimal(12,4) DEFAULT NULL COMMENT 'Total Offline Refunded',
  `total_online_refunded` decimal(12,4) DEFAULT NULL COMMENT 'Total Online Refunded',
  `total_paid` decimal(12,4) DEFAULT NULL COMMENT 'Total Paid',
  `total_qty_ordered` decimal(12,4) DEFAULT NULL COMMENT 'Total Qty Ordered',
  `total_refunded` decimal(12,4) DEFAULT NULL COMMENT 'Total Refunded',
  `can_ship_partially` smallint(5) UNSIGNED DEFAULT NULL COMMENT 'Can Ship Partially',
  `can_ship_partially_item` smallint(5) UNSIGNED DEFAULT NULL COMMENT 'Can Ship Partially Item',
  `customer_is_guest` smallint(5) UNSIGNED DEFAULT NULL COMMENT 'Customer Is Guest',
  `customer_note_notify` smallint(5) UNSIGNED DEFAULT NULL COMMENT 'Customer Note Notify',
  `billing_address_id` int(11) DEFAULT NULL COMMENT 'Billing Address Id',
  `customer_group_id` smallint(6) DEFAULT NULL COMMENT 'Customer Group Id',
  `edit_increment` int(11) DEFAULT NULL COMMENT 'Edit Increment',
  `email_sent` smallint(5) UNSIGNED DEFAULT NULL COMMENT 'Email Sent',
  `send_email` smallint(5) UNSIGNED DEFAULT NULL COMMENT 'Send Email',
  `forced_shipment_with_invoice` smallint(5) UNSIGNED DEFAULT NULL COMMENT 'Forced Do Shipment With Invoice',
  `payment_auth_expiration` int(11) DEFAULT NULL COMMENT 'Payment Authorization Expiration',
  `quote_address_id` int(11) DEFAULT NULL COMMENT 'Quote Address Id',
  `quote_id` int(11) DEFAULT NULL COMMENT 'Quote Id',
  `shipping_address_id` int(11) DEFAULT NULL COMMENT 'Shipping Address Id',
  `adjustment_negative` decimal(12,4) DEFAULT NULL COMMENT 'Adjustment Negative',
  `adjustment_positive` decimal(12,4) DEFAULT NULL COMMENT 'Adjustment Positive',
  `base_adjustment_negative` decimal(12,4) DEFAULT NULL COMMENT 'Base Adjustment Negative',
  `base_adjustment_positive` decimal(12,4) DEFAULT NULL COMMENT 'Base Adjustment Positive',
  `base_shipping_discount_amount` decimal(12,4) DEFAULT NULL COMMENT 'Base Shipping Discount Amount',
  `base_subtotal_incl_tax` decimal(12,4) DEFAULT NULL COMMENT 'Base Subtotal Incl Tax',
  `base_total_due` decimal(12,4) DEFAULT NULL COMMENT 'Base Total Due',
  `payment_authorization_amount` decimal(12,4) DEFAULT NULL COMMENT 'Payment Authorization Amount',
  `shipping_discount_amount` decimal(12,4) DEFAULT NULL COMMENT 'Shipping Discount Amount',
  `subtotal_incl_tax` decimal(12,4) DEFAULT NULL COMMENT 'Subtotal Incl Tax',
  `total_due` decimal(12,4) DEFAULT NULL COMMENT 'Total Due',
  `weight` decimal(12,4) DEFAULT NULL COMMENT 'Weight',
  `customer_dob` datetime DEFAULT NULL COMMENT 'Customer Dob',
  `increment_id` varchar(32) DEFAULT NULL COMMENT 'Increment Id',
  `applied_rule_ids` varchar(128) DEFAULT NULL COMMENT 'Applied Rule Ids',
  `base_currency_code` varchar(3) DEFAULT NULL COMMENT 'Base Currency Code',
  `customer_email` varchar(128) DEFAULT NULL COMMENT 'Customer Email',
  `customer_firstname` varchar(128) DEFAULT NULL COMMENT 'Customer Firstname',
  `customer_lastname` varchar(128) DEFAULT NULL COMMENT 'Customer Lastname',
  `customer_middlename` varchar(128) DEFAULT NULL COMMENT 'Customer Middlename',
  `customer_prefix` varchar(32) DEFAULT NULL COMMENT 'Customer Prefix',
  `customer_suffix` varchar(32) DEFAULT NULL COMMENT 'Customer Suffix',
  `customer_taxvat` varchar(32) DEFAULT NULL COMMENT 'Customer Taxvat',
  `discount_description` varchar(255) DEFAULT NULL COMMENT 'Discount Description',
  `ext_customer_id` varchar(32) DEFAULT NULL COMMENT 'Ext Customer Id',
  `ext_order_id` varchar(32) DEFAULT NULL COMMENT 'Ext Order Id',
  `global_currency_code` varchar(3) DEFAULT NULL COMMENT 'Global Currency Code',
  `hold_before_state` varchar(32) DEFAULT NULL COMMENT 'Hold Before State',
  `hold_before_status` varchar(32) DEFAULT NULL COMMENT 'Hold Before Status',
  `order_currency_code` varchar(3) DEFAULT NULL COMMENT 'Order Currency Code',
  `original_increment_id` varchar(32) DEFAULT NULL COMMENT 'Original Increment Id',
  `relation_child_id` varchar(32) DEFAULT NULL COMMENT 'Relation Child Id',
  `relation_child_real_id` varchar(32) DEFAULT NULL COMMENT 'Relation Child Real Id',
  `relation_parent_id` varchar(32) DEFAULT NULL COMMENT 'Relation Parent Id',
  `relation_parent_real_id` varchar(32) DEFAULT NULL COMMENT 'Relation Parent Real Id',
  `remote_ip` varchar(32) DEFAULT NULL COMMENT 'Remote Ip',
  `shipping_method` varchar(32) DEFAULT NULL COMMENT 'Shipping Method',
  `store_currency_code` varchar(3) DEFAULT NULL COMMENT 'Store Currency Code',
  `store_name` varchar(32) DEFAULT NULL COMMENT 'Store Name',
  `x_forwarded_for` varchar(32) DEFAULT NULL COMMENT 'X Forwarded For',
  `customer_note` text COMMENT 'Customer Note',
  `created_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT 'Created At',
  `updated_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP COMMENT 'Updated At',
  `total_item_count` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Total Item Count',
  `customer_gender` int(11) DEFAULT NULL COMMENT 'Customer Gender',
  `discount_tax_compensation_amount` decimal(12,4) DEFAULT NULL COMMENT 'Discount Tax Compensation Amount',
  `base_discount_tax_compensation_amount` decimal(12,4) DEFAULT NULL COMMENT 'Base Discount Tax Compensation Amount',
  `shipping_discount_tax_compensation_amount` decimal(12,4) DEFAULT NULL COMMENT 'Shipping Discount Tax Compensation Amount',
  `base_shipping_discount_tax_compensation_amnt` decimal(12,4) DEFAULT NULL COMMENT 'Base Shipping Discount Tax Compensation Amount',
  `discount_tax_compensation_invoiced` decimal(12,4) DEFAULT NULL COMMENT 'Discount Tax Compensation Invoiced',
  `base_discount_tax_compensation_invoiced` decimal(12,4) DEFAULT NULL COMMENT 'Base Discount Tax Compensation Invoiced',
  `discount_tax_compensation_refunded` decimal(12,4) DEFAULT NULL COMMENT 'Discount Tax Compensation Refunded',
  `base_discount_tax_compensation_refunded` decimal(12,4) DEFAULT NULL COMMENT 'Base Discount Tax Compensation Refunded',
  `shipping_incl_tax` decimal(12,4) DEFAULT NULL COMMENT 'Shipping Incl Tax',
  `base_shipping_incl_tax` decimal(12,4) DEFAULT NULL COMMENT 'Base Shipping Incl Tax',
  `coupon_rule_name` varchar(255) DEFAULT NULL COMMENT 'Coupon Sales Rule Name',
  `paypal_ipn_customer_notified` int(11) DEFAULT '0' COMMENT 'Paypal Ipn Customer Notified',
  `gift_message_id` int(11) DEFAULT NULL COMMENT 'Gift Message Id'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Sales Flat Order';

--
-- Dumping data for table `sales_order`
--

INSERT INTO `sales_order` (`entity_id`, `state`, `status`, `coupon_code`, `protect_code`, `shipping_description`, `is_virtual`, `store_id`, `customer_id`, `base_discount_amount`, `base_discount_canceled`, `base_discount_invoiced`, `base_discount_refunded`, `base_grand_total`, `base_shipping_amount`, `base_shipping_canceled`, `base_shipping_invoiced`, `base_shipping_refunded`, `base_shipping_tax_amount`, `base_shipping_tax_refunded`, `base_subtotal`, `base_subtotal_canceled`, `base_subtotal_invoiced`, `base_subtotal_refunded`, `base_tax_amount`, `base_tax_canceled`, `base_tax_invoiced`, `base_tax_refunded`, `base_to_global_rate`, `base_to_order_rate`, `base_total_canceled`, `base_total_invoiced`, `base_total_invoiced_cost`, `base_total_offline_refunded`, `base_total_online_refunded`, `base_total_paid`, `base_total_qty_ordered`, `base_total_refunded`, `discount_amount`, `discount_canceled`, `discount_invoiced`, `discount_refunded`, `grand_total`, `shipping_amount`, `shipping_canceled`, `shipping_invoiced`, `shipping_refunded`, `shipping_tax_amount`, `shipping_tax_refunded`, `store_to_base_rate`, `store_to_order_rate`, `subtotal`, `subtotal_canceled`, `subtotal_invoiced`, `subtotal_refunded`, `tax_amount`, `tax_canceled`, `tax_invoiced`, `tax_refunded`, `total_canceled`, `total_invoiced`, `total_offline_refunded`, `total_online_refunded`, `total_paid`, `total_qty_ordered`, `total_refunded`, `can_ship_partially`, `can_ship_partially_item`, `customer_is_guest`, `customer_note_notify`, `billing_address_id`, `customer_group_id`, `edit_increment`, `email_sent`, `send_email`, `forced_shipment_with_invoice`, `payment_auth_expiration`, `quote_address_id`, `quote_id`, `shipping_address_id`, `adjustment_negative`, `adjustment_positive`, `base_adjustment_negative`, `base_adjustment_positive`, `base_shipping_discount_amount`, `base_subtotal_incl_tax`, `base_total_due`, `payment_authorization_amount`, `shipping_discount_amount`, `subtotal_incl_tax`, `total_due`, `weight`, `customer_dob`, `increment_id`, `applied_rule_ids`, `base_currency_code`, `customer_email`, `customer_firstname`, `customer_lastname`, `customer_middlename`, `customer_prefix`, `customer_suffix`, `customer_taxvat`, `discount_description`, `ext_customer_id`, `ext_order_id`, `global_currency_code`, `hold_before_state`, `hold_before_status`, `order_currency_code`, `original_increment_id`, `relation_child_id`, `relation_child_real_id`, `relation_parent_id`, `relation_parent_real_id`, `remote_ip`, `shipping_method`, `store_currency_code`, `store_name`, `x_forwarded_for`, `customer_note`, `created_at`, `updated_at`, `total_item_count`, `customer_gender`, `discount_tax_compensation_amount`, `base_discount_tax_compensation_amount`, `shipping_discount_tax_compensation_amount`, `base_shipping_discount_tax_compensation_amnt`, `discount_tax_compensation_invoiced`, `base_discount_tax_compensation_invoiced`, `discount_tax_compensation_refunded`, `base_discount_tax_compensation_refunded`, `shipping_incl_tax`, `base_shipping_incl_tax`, `coupon_rule_name`, `paypal_ipn_customer_notified`, `gift_message_id`) VALUES
(1, 'new', 'pending', NULL, 'abe67e', NULL, 1, 1, 1, '0.0000', NULL, NULL, NULL, '120.0000', '0.0000', NULL, NULL, NULL, '0.0000', NULL, '120.0000', NULL, NULL, NULL, '0.0000', NULL, NULL, NULL, '1.0000', '1.0000', NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, '0.0000', NULL, NULL, NULL, '120.0000', '0.0000', NULL, NULL, NULL, '0.0000', NULL, '0.0000', '0.0000', '120.0000', NULL, NULL, NULL, '0.0000', NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, '1.0000', NULL, NULL, NULL, 1, 1, 1, 0, NULL, 1, 1, NULL, NULL, NULL, 7, NULL, NULL, NULL, NULL, NULL, '0.0000', '120.0000', '120.0000', NULL, '0.0000', '120.0000', '120.0000', '0.0000', NULL, '000000001', NULL, 'USD', 'lieult84@gmail.com', NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, 'USD', NULL, NULL, 'USD', NULL, NULL, NULL, NULL, NULL, '::1', NULL, 'USD', 'Main Website\r\nMain Website Store', NULL, NULL, '2016-04-27 08:10:33', '2016-04-27 08:11:04', 1, NULL, '0.0000', '0.0000', '0.0000', NULL, NULL, NULL, NULL, NULL, '0.0000', '0.0000', NULL, 0, NULL),
(2, 'new', 'pending', NULL, '9078af', NULL, 1, 1, NULL, '0.0000', NULL, NULL, NULL, '120.0000', '0.0000', NULL, NULL, NULL, '0.0000', NULL, '120.0000', NULL, NULL, NULL, '0.0000', NULL, NULL, NULL, '1.0000', '1.0000', NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, '0.0000', NULL, NULL, NULL, '120.0000', '0.0000', NULL, NULL, NULL, '0.0000', NULL, '0.0000', '0.0000', '120.0000', NULL, NULL, NULL, '0.0000', NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, '1.0000', NULL, NULL, NULL, 1, 1, 2, 0, NULL, 1, 1, NULL, NULL, NULL, 8, NULL, NULL, NULL, NULL, NULL, '0.0000', '120.0000', '120.0000', NULL, '0.0000', '120.0000', '120.0000', '0.0000', NULL, '000000002', NULL, 'USD', 'lieult84@gmail.com', NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, 'USD', NULL, NULL, 'USD', NULL, NULL, NULL, NULL, NULL, '::1', NULL, 'USD', 'Main Website\r\nMain Website Store', NULL, NULL, '2016-04-27 08:13:29', '2016-04-27 08:13:34', 1, NULL, '0.0000', '0.0000', '0.0000', NULL, NULL, NULL, NULL, NULL, '0.0000', '0.0000', NULL, 0, NULL),
(3, 'new', 'pending', NULL, 'd23271', NULL, 1, 1, NULL, '0.0000', NULL, NULL, NULL, '49.0000', '0.0000', NULL, NULL, NULL, '0.0000', NULL, '49.0000', NULL, NULL, NULL, '0.0000', NULL, NULL, NULL, '1.0000', '1.0000', NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, '0.0000', NULL, NULL, NULL, '49.0000', '0.0000', NULL, NULL, NULL, '0.0000', NULL, '0.0000', '0.0000', '49.0000', NULL, NULL, NULL, '0.0000', NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, '2.0000', NULL, NULL, NULL, 1, 1, 3, 0, NULL, 1, 1, NULL, NULL, NULL, 9, NULL, NULL, NULL, NULL, NULL, '0.0000', '49.0000', '49.0000', NULL, '0.0000', '49.0000', '49.0000', '0.0000', NULL, '000000003', NULL, 'USD', 'lieult84@gmail.com', NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, 'USD', NULL, NULL, 'USD', NULL, NULL, NULL, NULL, NULL, '::1', NULL, 'USD', 'Main Website\r\nMain Website Store', NULL, NULL, '2016-04-27 08:15:54', '2016-04-27 08:15:58', 2, NULL, '0.0000', '0.0000', '0.0000', NULL, NULL, NULL, NULL, NULL, '0.0000', '0.0000', NULL, 0, NULL),
(4, 'new', 'pending', NULL, '2bfc6a', NULL, 1, 1, 2, '0.0000', NULL, NULL, NULL, '169.0000', '0.0000', NULL, NULL, NULL, '0.0000', NULL, '169.0000', NULL, NULL, NULL, '0.0000', NULL, NULL, NULL, '1.0000', '1.0000', NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, '0.0000', NULL, NULL, NULL, '169.0000', '0.0000', NULL, NULL, NULL, '0.0000', NULL, '0.0000', '0.0000', '169.0000', NULL, NULL, NULL, '0.0000', NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, '3.0000', NULL, NULL, NULL, 0, 1, 4, 1, NULL, 1, 1, NULL, NULL, NULL, 11, NULL, NULL, NULL, NULL, NULL, '0.0000', '169.0000', '169.0000', NULL, '0.0000', '169.0000', '169.0000', '0.0000', NULL, '000000004', NULL, 'USD', 'lieult84@yahoo.com', 'Le', 'Lieu', NULL, NULL, NULL, NULL, NULL, NULL, NULL, 'USD', NULL, NULL, 'USD', NULL, NULL, NULL, NULL, NULL, '::1', NULL, 'USD', 'Main Website\r\nMain Website Store', NULL, NULL, '2016-04-28 03:06:22', '2016-04-28 03:06:28', 3, NULL, '0.0000', '0.0000', '0.0000', NULL, NULL, NULL, NULL, NULL, '0.0000', '0.0000', NULL, 0, NULL);

-- --------------------------------------------------------

--
-- Table structure for table `sales_order_address`
--

CREATE TABLE `sales_order_address` (
  `entity_id` int(10) UNSIGNED NOT NULL COMMENT 'Entity Id',
  `parent_id` int(10) UNSIGNED DEFAULT NULL COMMENT 'Parent Id',
  `customer_address_id` int(11) DEFAULT NULL COMMENT 'Customer Address Id',
  `quote_address_id` int(11) DEFAULT NULL COMMENT 'Quote Address Id',
  `region_id` int(11) DEFAULT NULL COMMENT 'Region Id',
  `customer_id` int(11) DEFAULT NULL COMMENT 'Customer Id',
  `fax` varchar(255) DEFAULT NULL COMMENT 'Fax',
  `region` varchar(255) DEFAULT NULL COMMENT 'Region',
  `postcode` varchar(255) DEFAULT NULL COMMENT 'Postcode',
  `lastname` varchar(255) DEFAULT NULL COMMENT 'Lastname',
  `street` varchar(255) DEFAULT NULL COMMENT 'Street',
  `city` varchar(255) DEFAULT NULL COMMENT 'City',
  `email` varchar(255) DEFAULT NULL COMMENT 'Email',
  `telephone` varchar(255) DEFAULT NULL COMMENT 'Phone Number',
  `country_id` varchar(2) DEFAULT NULL COMMENT 'Country Id',
  `firstname` varchar(255) DEFAULT NULL COMMENT 'Firstname',
  `address_type` varchar(255) DEFAULT NULL COMMENT 'Address Type',
  `prefix` varchar(255) DEFAULT NULL COMMENT 'Prefix',
  `middlename` varchar(255) DEFAULT NULL COMMENT 'Middlename',
  `suffix` varchar(255) DEFAULT NULL COMMENT 'Suffix',
  `company` varchar(255) DEFAULT NULL COMMENT 'Company',
  `vat_id` text COMMENT 'Vat Id',
  `vat_is_valid` smallint(6) DEFAULT NULL COMMENT 'Vat Is Valid',
  `vat_request_id` text COMMENT 'Vat Request Id',
  `vat_request_date` text COMMENT 'Vat Request Date',
  `vat_request_success` smallint(6) DEFAULT NULL COMMENT 'Vat Request Success'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Sales Flat Order Address';

--
-- Dumping data for table `sales_order_address`
--

INSERT INTO `sales_order_address` (`entity_id`, `parent_id`, `customer_address_id`, `quote_address_id`, `region_id`, `customer_id`, `fax`, `region`, `postcode`, `lastname`, `street`, `city`, `email`, `telephone`, `country_id`, `firstname`, `address_type`, `prefix`, `middlename`, `suffix`, `company`, `vat_id`, `vat_is_valid`, `vat_request_id`, `vat_request_date`, `vat_request_success`) VALUES
(1, 1, NULL, NULL, 1, NULL, NULL, 'Alabama', '12345', 'Lieu', 'MD', 'Ha Noi', 'lieult84@gmail.com', '123456789', 'US', 'Le', 'billing', NULL, NULL, NULL, 'Brainos', NULL, NULL, NULL, NULL, NULL),
(2, 2, NULL, NULL, 1, NULL, NULL, 'Alabama', '12345', 'Lieu', 'MD', 'Ha Noi', 'lieult84@gmail.com', '123456789', 'US', 'Le ', 'billing', NULL, NULL, NULL, 'Brainos', NULL, NULL, NULL, NULL, NULL),
(3, 3, NULL, NULL, 1, NULL, NULL, 'Alabama', '12345', 'Lieu', 'MD', 'Ha Noi', 'lieult84@gmail.com', '123456789', 'US', 'Le', 'billing', NULL, NULL, NULL, 'Brainos', NULL, NULL, NULL, NULL, NULL),
(4, 4, NULL, NULL, 1, NULL, NULL, 'Alabama', '12345', 'Lieu', 'MD', 'Ha Noi', 'lieult84@yahoo.com', '123456789', 'US', 'Le', 'billing', NULL, NULL, NULL, 'TNT', NULL, NULL, NULL, NULL, NULL);

-- --------------------------------------------------------

--
-- Table structure for table `sales_order_aggregated_created`
--

CREATE TABLE `sales_order_aggregated_created` (
  `id` int(10) UNSIGNED NOT NULL COMMENT 'Id',
  `period` date DEFAULT NULL COMMENT 'Period',
  `store_id` smallint(5) UNSIGNED DEFAULT NULL COMMENT 'Store Id',
  `order_status` varchar(50) NOT NULL COMMENT 'Order Status',
  `orders_count` int(11) NOT NULL DEFAULT '0' COMMENT 'Orders Count',
  `total_qty_ordered` decimal(12,4) NOT NULL DEFAULT '0.0000' COMMENT 'Total Qty Ordered',
  `total_qty_invoiced` decimal(12,4) NOT NULL DEFAULT '0.0000' COMMENT 'Total Qty Invoiced',
  `total_income_amount` decimal(12,4) NOT NULL DEFAULT '0.0000' COMMENT 'Total Income Amount',
  `total_revenue_amount` decimal(12,4) NOT NULL DEFAULT '0.0000' COMMENT 'Total Revenue Amount',
  `total_profit_amount` decimal(12,4) NOT NULL DEFAULT '0.0000' COMMENT 'Total Profit Amount',
  `total_invoiced_amount` decimal(12,4) NOT NULL DEFAULT '0.0000' COMMENT 'Total Invoiced Amount',
  `total_canceled_amount` decimal(12,4) NOT NULL DEFAULT '0.0000' COMMENT 'Total Canceled Amount',
  `total_paid_amount` decimal(12,4) NOT NULL DEFAULT '0.0000' COMMENT 'Total Paid Amount',
  `total_refunded_amount` decimal(12,4) NOT NULL DEFAULT '0.0000' COMMENT 'Total Refunded Amount',
  `total_tax_amount` decimal(12,4) NOT NULL DEFAULT '0.0000' COMMENT 'Total Tax Amount',
  `total_tax_amount_actual` decimal(12,4) NOT NULL DEFAULT '0.0000' COMMENT 'Total Tax Amount Actual',
  `total_shipping_amount` decimal(12,4) NOT NULL DEFAULT '0.0000' COMMENT 'Total Shipping Amount',
  `total_shipping_amount_actual` decimal(12,4) NOT NULL DEFAULT '0.0000' COMMENT 'Total Shipping Amount Actual',
  `total_discount_amount` decimal(12,4) NOT NULL DEFAULT '0.0000' COMMENT 'Total Discount Amount',
  `total_discount_amount_actual` decimal(12,4) NOT NULL DEFAULT '0.0000' COMMENT 'Total Discount Amount Actual'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Sales Order Aggregated Created';

-- --------------------------------------------------------

--
-- Table structure for table `sales_order_aggregated_updated`
--

CREATE TABLE `sales_order_aggregated_updated` (
  `id` int(10) UNSIGNED NOT NULL COMMENT 'Id',
  `period` date DEFAULT NULL COMMENT 'Period',
  `store_id` smallint(5) UNSIGNED DEFAULT NULL COMMENT 'Store Id',
  `order_status` varchar(50) NOT NULL COMMENT 'Order Status',
  `orders_count` int(11) NOT NULL DEFAULT '0' COMMENT 'Orders Count',
  `total_qty_ordered` decimal(12,4) NOT NULL DEFAULT '0.0000' COMMENT 'Total Qty Ordered',
  `total_qty_invoiced` decimal(12,4) NOT NULL DEFAULT '0.0000' COMMENT 'Total Qty Invoiced',
  `total_income_amount` decimal(12,4) NOT NULL DEFAULT '0.0000' COMMENT 'Total Income Amount',
  `total_revenue_amount` decimal(12,4) NOT NULL DEFAULT '0.0000' COMMENT 'Total Revenue Amount',
  `total_profit_amount` decimal(12,4) NOT NULL DEFAULT '0.0000' COMMENT 'Total Profit Amount',
  `total_invoiced_amount` decimal(12,4) NOT NULL DEFAULT '0.0000' COMMENT 'Total Invoiced Amount',
  `total_canceled_amount` decimal(12,4) NOT NULL DEFAULT '0.0000' COMMENT 'Total Canceled Amount',
  `total_paid_amount` decimal(12,4) NOT NULL DEFAULT '0.0000' COMMENT 'Total Paid Amount',
  `total_refunded_amount` decimal(12,4) NOT NULL DEFAULT '0.0000' COMMENT 'Total Refunded Amount',
  `total_tax_amount` decimal(12,4) NOT NULL DEFAULT '0.0000' COMMENT 'Total Tax Amount',
  `total_tax_amount_actual` decimal(12,4) NOT NULL DEFAULT '0.0000' COMMENT 'Total Tax Amount Actual',
  `total_shipping_amount` decimal(12,4) NOT NULL DEFAULT '0.0000' COMMENT 'Total Shipping Amount',
  `total_shipping_amount_actual` decimal(12,4) NOT NULL DEFAULT '0.0000' COMMENT 'Total Shipping Amount Actual',
  `total_discount_amount` decimal(12,4) NOT NULL DEFAULT '0.0000' COMMENT 'Total Discount Amount',
  `total_discount_amount_actual` decimal(12,4) NOT NULL DEFAULT '0.0000' COMMENT 'Total Discount Amount Actual'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Sales Order Aggregated Updated';

-- --------------------------------------------------------

--
-- Table structure for table `sales_order_grid`
--

CREATE TABLE `sales_order_grid` (
  `entity_id` int(10) UNSIGNED NOT NULL COMMENT 'Entity Id',
  `status` varchar(32) DEFAULT NULL COMMENT 'Status',
  `store_id` smallint(5) UNSIGNED DEFAULT NULL COMMENT 'Store Id',
  `store_name` varchar(255) DEFAULT NULL COMMENT 'Store Name',
  `customer_id` int(10) UNSIGNED DEFAULT NULL COMMENT 'Customer Id',
  `base_grand_total` decimal(12,4) DEFAULT NULL COMMENT 'Base Grand Total',
  `base_total_paid` decimal(12,4) DEFAULT NULL COMMENT 'Base Total Paid',
  `grand_total` decimal(12,4) DEFAULT NULL COMMENT 'Grand Total',
  `total_paid` decimal(12,4) DEFAULT NULL COMMENT 'Total Paid',
  `increment_id` varchar(50) DEFAULT NULL COMMENT 'Increment Id',
  `base_currency_code` varchar(3) DEFAULT NULL COMMENT 'Base Currency Code',
  `order_currency_code` varchar(255) DEFAULT NULL COMMENT 'Order Currency Code',
  `shipping_name` varchar(255) DEFAULT NULL COMMENT 'Shipping Name',
  `billing_name` varchar(255) DEFAULT NULL COMMENT 'Billing Name',
  `created_at` timestamp NULL DEFAULT NULL COMMENT 'Created At',
  `updated_at` timestamp NULL DEFAULT NULL COMMENT 'Updated At',
  `billing_address` varchar(255) DEFAULT NULL COMMENT 'Billing Address',
  `shipping_address` varchar(255) DEFAULT NULL COMMENT 'Shipping Address',
  `shipping_information` varchar(255) DEFAULT NULL COMMENT 'Shipping Method Name',
  `customer_email` varchar(255) DEFAULT NULL COMMENT 'Customer Email',
  `customer_group` varchar(255) DEFAULT NULL COMMENT 'Customer Group',
  `subtotal` decimal(12,4) DEFAULT NULL COMMENT 'Subtotal',
  `shipping_and_handling` decimal(12,4) DEFAULT NULL COMMENT 'Shipping and handling amount',
  `customer_name` varchar(255) DEFAULT NULL COMMENT 'Customer Name',
  `payment_method` varchar(255) DEFAULT NULL COMMENT 'Payment Method',
  `total_refunded` decimal(12,4) DEFAULT NULL COMMENT 'Total Refunded'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Sales Flat Order Grid';

--
-- Dumping data for table `sales_order_grid`
--

INSERT INTO `sales_order_grid` (`entity_id`, `status`, `store_id`, `store_name`, `customer_id`, `base_grand_total`, `base_total_paid`, `grand_total`, `total_paid`, `increment_id`, `base_currency_code`, `order_currency_code`, `shipping_name`, `billing_name`, `created_at`, `updated_at`, `billing_address`, `shipping_address`, `shipping_information`, `customer_email`, `customer_group`, `subtotal`, `shipping_and_handling`, `customer_name`, `payment_method`, `total_refunded`) VALUES
(1, 'pending', 1, 'Main Website\r\nMain Website Store', 1, '120.0000', NULL, '120.0000', NULL, '000000001', 'USD', 'USD', '', 'Le Lieu', '2016-04-27 08:10:33', '2016-04-27 08:11:04', 'MD Ha Noi Alabama 12345', '', NULL, 'lieult84@gmail.com', '0', '120.0000', '0.0000', '', 'checkmo', NULL),
(2, 'pending', 1, 'Main Website\r\nMain Website Store', NULL, '120.0000', NULL, '120.0000', NULL, '000000002', 'USD', 'USD', '', 'Le  Lieu', '2016-04-27 08:13:29', '2016-04-27 08:13:29', 'MD Ha Noi Alabama 12345', '', NULL, 'lieult84@gmail.com', '0', '120.0000', '0.0000', '', 'checkmo', NULL),
(3, 'pending', 1, 'Main Website\r\nMain Website Store', NULL, '49.0000', NULL, '49.0000', NULL, '000000003', 'USD', 'USD', '', 'Le Lieu', '2016-04-27 08:15:54', '2016-04-27 08:15:54', 'MD Ha Noi Alabama 12345', '', NULL, 'lieult84@gmail.com', '0', '49.0000', '0.0000', '', 'checkmo', NULL),
(4, 'pending', 1, 'Main Website\r\nMain Website Store', 2, '169.0000', NULL, '169.0000', NULL, '000000004', 'USD', 'USD', '', 'Le Lieu', '2016-04-28 03:06:22', '2016-04-28 03:06:22', 'MD Ha Noi Alabama 12345', '', NULL, 'lieult84@yahoo.com', '1', '169.0000', '0.0000', 'Le Lieu', 'checkmo', NULL);

-- --------------------------------------------------------

--
-- Table structure for table `sales_order_item`
--

CREATE TABLE `sales_order_item` (
  `item_id` int(10) UNSIGNED NOT NULL COMMENT 'Item Id',
  `order_id` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Order Id',
  `parent_item_id` int(10) UNSIGNED DEFAULT NULL COMMENT 'Parent Item Id',
  `quote_item_id` int(10) UNSIGNED DEFAULT NULL COMMENT 'Quote Item Id',
  `store_id` smallint(5) UNSIGNED DEFAULT NULL COMMENT 'Store Id',
  `created_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT 'Created At',
  `updated_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP COMMENT 'Updated At',
  `product_id` int(10) UNSIGNED DEFAULT NULL COMMENT 'Product Id',
  `product_type` varchar(255) DEFAULT NULL COMMENT 'Product Type',
  `product_options` text COMMENT 'Product Options',
  `weight` decimal(12,4) DEFAULT '0.0000' COMMENT 'Weight',
  `is_virtual` smallint(5) UNSIGNED DEFAULT NULL COMMENT 'Is Virtual',
  `sku` varchar(255) DEFAULT NULL COMMENT 'Sku',
  `name` varchar(255) DEFAULT NULL COMMENT 'Name',
  `description` text COMMENT 'Description',
  `applied_rule_ids` text COMMENT 'Applied Rule Ids',
  `additional_data` text COMMENT 'Additional Data',
  `is_qty_decimal` smallint(5) UNSIGNED DEFAULT NULL COMMENT 'Is Qty Decimal',
  `no_discount` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'No Discount',
  `qty_backordered` decimal(12,4) DEFAULT '0.0000' COMMENT 'Qty Backordered',
  `qty_canceled` decimal(12,4) DEFAULT '0.0000' COMMENT 'Qty Canceled',
  `qty_invoiced` decimal(12,4) DEFAULT '0.0000' COMMENT 'Qty Invoiced',
  `qty_ordered` decimal(12,4) DEFAULT '0.0000' COMMENT 'Qty Ordered',
  `qty_refunded` decimal(12,4) DEFAULT '0.0000' COMMENT 'Qty Refunded',
  `qty_shipped` decimal(12,4) DEFAULT '0.0000' COMMENT 'Qty Shipped',
  `base_cost` decimal(12,4) DEFAULT '0.0000' COMMENT 'Base Cost',
  `price` decimal(12,4) NOT NULL DEFAULT '0.0000' COMMENT 'Price',
  `base_price` decimal(12,4) NOT NULL DEFAULT '0.0000' COMMENT 'Base Price',
  `original_price` decimal(12,4) DEFAULT NULL COMMENT 'Original Price',
  `base_original_price` decimal(12,4) DEFAULT NULL COMMENT 'Base Original Price',
  `tax_percent` decimal(12,4) DEFAULT '0.0000' COMMENT 'Tax Percent',
  `tax_amount` decimal(12,4) DEFAULT '0.0000' COMMENT 'Tax Amount',
  `base_tax_amount` decimal(12,4) DEFAULT '0.0000' COMMENT 'Base Tax Amount',
  `tax_invoiced` decimal(12,4) DEFAULT '0.0000' COMMENT 'Tax Invoiced',
  `base_tax_invoiced` decimal(12,4) DEFAULT '0.0000' COMMENT 'Base Tax Invoiced',
  `discount_percent` decimal(12,4) DEFAULT '0.0000' COMMENT 'Discount Percent',
  `discount_amount` decimal(12,4) DEFAULT '0.0000' COMMENT 'Discount Amount',
  `base_discount_amount` decimal(12,4) DEFAULT '0.0000' COMMENT 'Base Discount Amount',
  `discount_invoiced` decimal(12,4) DEFAULT '0.0000' COMMENT 'Discount Invoiced',
  `base_discount_invoiced` decimal(12,4) DEFAULT '0.0000' COMMENT 'Base Discount Invoiced',
  `amount_refunded` decimal(12,4) DEFAULT '0.0000' COMMENT 'Amount Refunded',
  `base_amount_refunded` decimal(12,4) DEFAULT '0.0000' COMMENT 'Base Amount Refunded',
  `row_total` decimal(12,4) NOT NULL DEFAULT '0.0000' COMMENT 'Row Total',
  `base_row_total` decimal(12,4) NOT NULL DEFAULT '0.0000' COMMENT 'Base Row Total',
  `row_invoiced` decimal(12,4) NOT NULL DEFAULT '0.0000' COMMENT 'Row Invoiced',
  `base_row_invoiced` decimal(12,4) NOT NULL DEFAULT '0.0000' COMMENT 'Base Row Invoiced',
  `row_weight` decimal(12,4) DEFAULT '0.0000' COMMENT 'Row Weight',
  `base_tax_before_discount` decimal(12,4) DEFAULT NULL COMMENT 'Base Tax Before Discount',
  `tax_before_discount` decimal(12,4) DEFAULT NULL COMMENT 'Tax Before Discount',
  `ext_order_item_id` varchar(255) DEFAULT NULL COMMENT 'Ext Order Item Id',
  `locked_do_invoice` smallint(5) UNSIGNED DEFAULT NULL COMMENT 'Locked Do Invoice',
  `locked_do_ship` smallint(5) UNSIGNED DEFAULT NULL COMMENT 'Locked Do Ship',
  `price_incl_tax` decimal(12,4) DEFAULT NULL COMMENT 'Price Incl Tax',
  `base_price_incl_tax` decimal(12,4) DEFAULT NULL COMMENT 'Base Price Incl Tax',
  `row_total_incl_tax` decimal(12,4) DEFAULT NULL COMMENT 'Row Total Incl Tax',
  `base_row_total_incl_tax` decimal(12,4) DEFAULT NULL COMMENT 'Base Row Total Incl Tax',
  `discount_tax_compensation_amount` decimal(12,4) DEFAULT NULL COMMENT 'Discount Tax Compensation Amount',
  `base_discount_tax_compensation_amount` decimal(12,4) DEFAULT NULL COMMENT 'Base Discount Tax Compensation Amount',
  `discount_tax_compensation_invoiced` decimal(12,4) DEFAULT NULL COMMENT 'Discount Tax Compensation Invoiced',
  `base_discount_tax_compensation_invoiced` decimal(12,4) DEFAULT NULL COMMENT 'Base Discount Tax Compensation Invoiced',
  `discount_tax_compensation_refunded` decimal(12,4) DEFAULT NULL COMMENT 'Discount Tax Compensation Refunded',
  `base_discount_tax_compensation_refunded` decimal(12,4) DEFAULT NULL COMMENT 'Base Discount Tax Compensation Refunded',
  `tax_canceled` decimal(12,4) DEFAULT NULL COMMENT 'Tax Canceled',
  `discount_tax_compensation_canceled` decimal(12,4) DEFAULT NULL COMMENT 'Discount Tax Compensation Canceled',
  `tax_refunded` decimal(12,4) DEFAULT NULL COMMENT 'Tax Refunded',
  `base_tax_refunded` decimal(12,4) DEFAULT NULL COMMENT 'Base Tax Refunded',
  `discount_refunded` decimal(12,4) DEFAULT NULL COMMENT 'Discount Refunded',
  `base_discount_refunded` decimal(12,4) DEFAULT NULL COMMENT 'Base Discount Refunded',
  `free_shipping` smallint(6) DEFAULT NULL,
  `gift_message_id` int(11) DEFAULT NULL COMMENT 'Gift Message Id',
  `gift_message_available` int(11) DEFAULT NULL COMMENT 'Gift Message Available',
  `weee_tax_applied` text COMMENT 'Weee Tax Applied',
  `weee_tax_applied_amount` decimal(12,4) DEFAULT NULL COMMENT 'Weee Tax Applied Amount',
  `weee_tax_applied_row_amount` decimal(12,4) DEFAULT NULL COMMENT 'Weee Tax Applied Row Amount',
  `weee_tax_disposition` decimal(12,4) DEFAULT NULL COMMENT 'Weee Tax Disposition',
  `weee_tax_row_disposition` decimal(12,4) DEFAULT NULL COMMENT 'Weee Tax Row Disposition',
  `base_weee_tax_applied_amount` decimal(12,4) DEFAULT NULL COMMENT 'Base Weee Tax Applied Amount',
  `base_weee_tax_applied_row_amnt` decimal(12,4) DEFAULT NULL COMMENT 'Base Weee Tax Applied Row Amnt',
  `base_weee_tax_disposition` decimal(12,4) DEFAULT NULL COMMENT 'Base Weee Tax Disposition',
  `base_weee_tax_row_disposition` decimal(12,4) DEFAULT NULL COMMENT 'Base Weee Tax Row Disposition'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Sales Flat Order Item';

--
-- Dumping data for table `sales_order_item`
--

INSERT INTO `sales_order_item` (`item_id`, `order_id`, `parent_item_id`, `quote_item_id`, `store_id`, `created_at`, `updated_at`, `product_id`, `product_type`, `product_options`, `weight`, `is_virtual`, `sku`, `name`, `description`, `applied_rule_ids`, `additional_data`, `is_qty_decimal`, `no_discount`, `qty_backordered`, `qty_canceled`, `qty_invoiced`, `qty_ordered`, `qty_refunded`, `qty_shipped`, `base_cost`, `price`, `base_price`, `original_price`, `base_original_price`, `tax_percent`, `tax_amount`, `base_tax_amount`, `tax_invoiced`, `base_tax_invoiced`, `discount_percent`, `discount_amount`, `base_discount_amount`, `discount_invoiced`, `base_discount_invoiced`, `amount_refunded`, `base_amount_refunded`, `row_total`, `base_row_total`, `row_invoiced`, `base_row_invoiced`, `row_weight`, `base_tax_before_discount`, `tax_before_discount`, `ext_order_item_id`, `locked_do_invoice`, `locked_do_ship`, `price_incl_tax`, `base_price_incl_tax`, `row_total_incl_tax`, `base_row_total_incl_tax`, `discount_tax_compensation_amount`, `base_discount_tax_compensation_amount`, `discount_tax_compensation_invoiced`, `base_discount_tax_compensation_invoiced`, `discount_tax_compensation_refunded`, `base_discount_tax_compensation_refunded`, `tax_canceled`, `discount_tax_compensation_canceled`, `tax_refunded`, `base_tax_refunded`, `discount_refunded`, `base_discount_refunded`, `free_shipping`, `gift_message_id`, `gift_message_available`, `weee_tax_applied`, `weee_tax_applied_amount`, `weee_tax_applied_row_amount`, `weee_tax_disposition`, `weee_tax_row_disposition`, `base_weee_tax_applied_amount`, `base_weee_tax_applied_row_amnt`, `base_weee_tax_disposition`, `base_weee_tax_row_disposition`) VALUES
(1, 1, NULL, 14, 1, '2016-04-27 08:10:33', '2016-04-27 08:10:33', 9, 'bundle', 'a:4:{s:15:"info_buyRequest";a:6:{s:4:"uenc";s:80:"aHR0cDovL2xvY2FsaG9zdC92ZXNfZmFzb255L21hZ2VudG8tYnVuZGxlLXByb2R1Y3QtdHlwZS5odG1s";s:7:"product";s:1:"9";s:28:"selected_configurable_option";s:0:"";s:15:"related_product";s:0:"";s:13:"bundle_option";a:1:{i:1;a:1:{i:6;s:1:"2";}}s:3:"qty";s:1:"1";}s:14:"bundle_options";a:1:{i:1;a:3:{s:9:"option_id";s:1:"1";s:5:"label";s:18:"Custom option name";s:5:"value";a:1:{i:0;a:3:{s:5:"title";s:34:"product configuration magento-blue";s:3:"qty";i:1;s:5:"price";d:120;}}}}s:20:"product_calculations";i:0;s:13:"shipment_type";s:1:"0";}', '0.0000', 1, 'Magento Bundle Product Type-product configuration magento-blue', 'Magento Bundle Product Type', NULL, NULL, NULL, 0, 0, NULL, '0.0000', '0.0000', '1.0000', '0.0000', '0.0000', NULL, '120.0000', '120.0000', '120.0000', '120.0000', NULL, '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '120.0000', '120.0000', '0.0000', '0.0000', '0.0000', NULL, NULL, NULL, NULL, NULL, '120.0000', '120.0000', '120.0000', '120.0000', NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, 0, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL),
(2, 1, 1, 15, 1, '2016-04-27 08:10:33', '2016-04-27 08:10:33', 6, 'virtual', 'a:2:{s:15:"info_buyRequest";a:6:{s:4:"uenc";s:80:"aHR0cDovL2xvY2FsaG9zdC92ZXNfZmFzb255L21hZ2VudG8tYnVuZGxlLXByb2R1Y3QtdHlwZS5odG1s";s:7:"product";s:1:"9";s:28:"selected_configurable_option";s:0:"";s:15:"related_product";s:0:"";s:13:"bundle_option";a:1:{i:1;a:1:{i:6;s:1:"2";}}s:3:"qty";s:1:"1";}s:27:"bundle_selection_attributes";s:108:"a:4:{s:5:"price";d:120;s:3:"qty";d:1;s:12:"option_label";s:18:"Custom option name";s:9:"option_id";s:1:"1";}";}', NULL, 1, 'product configuration magento-blue', 'product configuration magento-blue', NULL, NULL, NULL, 0, 0, NULL, '0.0000', '0.0000', '1.0000', '0.0000', '0.0000', NULL, '120.0000', '120.0000', '120.0000', '120.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '120.0000', '120.0000', '0.0000', '0.0000', '0.0000', NULL, NULL, NULL, NULL, NULL, '120.0000', '120.0000', '120.0000', '120.0000', '0.0000', '0.0000', NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, 0, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL),
(3, 2, NULL, 16, 1, '2016-04-27 08:13:29', '2016-04-27 08:13:29', 5, 'configurable', 'a:6:{s:15:"info_buyRequest";a:6:{s:4:"uenc";s:84:"aHR0cDovL2xvY2FsaG9zdC92ZXNfZmFzb255L3Byb2R1Y3QtY29uZmlndXJhdGlvbi1tYWdlbnRvLmh0bWw,";s:7:"product";s:1:"5";s:28:"selected_configurable_option";s:1:"6";s:15:"related_product";s:0:"";s:15:"super_attribute";a:1:{i:90;s:1:"4";}s:3:"qty";s:1:"1";}s:15:"attributes_info";a:1:{i:0;a:2:{s:5:"label";s:5:"Color";s:5:"value";s:4:"blue";}}s:11:"simple_name";s:34:"product configuration magento-blue";s:10:"simple_sku";s:34:"product configuration magento-blue";s:20:"product_calculations";i:1;s:13:"shipment_type";i:0;}', NULL, 1, 'product configuration magento-blue', 'product configuration magento', NULL, NULL, NULL, 0, 0, NULL, '0.0000', '0.0000', '1.0000', '0.0000', '0.0000', NULL, '120.0000', '120.0000', '120.0000', '120.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '120.0000', '120.0000', '0.0000', '0.0000', '0.0000', NULL, NULL, NULL, NULL, NULL, '120.0000', '120.0000', '120.0000', '120.0000', '0.0000', '0.0000', NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, 0, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL),
(4, 2, 3, 17, 1, '2016-04-27 08:13:29', '2016-04-27 08:13:29', 6, 'virtual', 'a:1:{s:15:"info_buyRequest";a:6:{s:4:"uenc";s:84:"aHR0cDovL2xvY2FsaG9zdC92ZXNfZmFzb255L3Byb2R1Y3QtY29uZmlndXJhdGlvbi1tYWdlbnRvLmh0bWw,";s:7:"product";s:1:"5";s:28:"selected_configurable_option";s:1:"6";s:15:"related_product";s:0:"";s:15:"super_attribute";a:1:{i:90;s:1:"4";}s:3:"qty";s:1:"1";}}', NULL, 1, 'product configuration magento-blue', 'product configuration magento-blue', NULL, NULL, NULL, 0, 0, NULL, '0.0000', '0.0000', '1.0000', '0.0000', '0.0000', NULL, '0.0000', '0.0000', '0.0000', NULL, '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, 0, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL),
(5, 3, NULL, 18, 1, '2016-04-27 08:15:54', '2016-04-27 08:15:54', 3, 'grouped', 'a:2:{s:15:"info_buyRequest";a:1:{s:20:"super_product_config";a:2:{s:12:"product_type";s:7:"grouped";s:10:"product_id";s:2:"10";}}s:20:"super_product_config";a:3:{s:12:"product_code";s:12:"product_type";s:12:"product_type";s:7:"grouped";s:10:"product_id";s:2:"10";}}', NULL, 1, 'Atomic Endurance Running Tee', 'Atomic Endurance Running Tee', NULL, NULL, NULL, 0, 0, NULL, '0.0000', '0.0000', '1.0000', '0.0000', '0.0000', NULL, '25.0000', '25.0000', '25.0000', '25.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '25.0000', '25.0000', '0.0000', '0.0000', '0.0000', NULL, NULL, NULL, NULL, NULL, '25.0000', '25.0000', '25.0000', '25.0000', '0.0000', '0.0000', NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, 0, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL),
(6, 3, NULL, 19, 1, '2016-04-27 08:15:54', '2016-04-27 08:15:54', 4, 'grouped', 'a:2:{s:15:"info_buyRequest";a:1:{s:20:"super_product_config";a:2:{s:12:"product_type";s:7:"grouped";s:10:"product_id";s:2:"10";}}s:20:"super_product_config";a:3:{s:12:"product_code";s:12:"product_type";s:12:"product_type";s:7:"grouped";s:10:"product_id";s:2:"10";}}', NULL, 1, 'Arcadio Gym Short', 'Arcadio Gym Short', NULL, NULL, NULL, 0, 0, NULL, '0.0000', '0.0000', '1.0000', '0.0000', '0.0000', NULL, '24.0000', '24.0000', '24.0000', '24.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '24.0000', '24.0000', '0.0000', '0.0000', '0.0000', NULL, NULL, NULL, NULL, NULL, '24.0000', '24.0000', '24.0000', '24.0000', '0.0000', '0.0000', NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, 0, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL),
(7, 4, NULL, 21, 1, '2016-04-28 03:06:22', '2016-04-28 03:06:22', 3, 'grouped', 'a:2:{s:15:"info_buyRequest";a:1:{s:20:"super_product_config";a:2:{s:12:"product_type";s:7:"grouped";s:10:"product_id";s:2:"10";}}s:20:"super_product_config";a:3:{s:12:"product_code";s:12:"product_type";s:12:"product_type";s:7:"grouped";s:10:"product_id";s:2:"10";}}', NULL, 1, 'Atomic Endurance Running Tee', 'Atomic Endurance Running Tee', NULL, NULL, NULL, 0, 0, NULL, '0.0000', '0.0000', '1.0000', '0.0000', '0.0000', NULL, '25.0000', '25.0000', '25.0000', '25.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '25.0000', '25.0000', '0.0000', '0.0000', '0.0000', NULL, NULL, NULL, NULL, NULL, '25.0000', '25.0000', '25.0000', '25.0000', '0.0000', '0.0000', NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, 0, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL),
(8, 4, NULL, 22, 1, '2016-04-28 03:06:22', '2016-04-28 03:06:22', 4, 'grouped', 'a:2:{s:15:"info_buyRequest";a:1:{s:20:"super_product_config";a:2:{s:12:"product_type";s:7:"grouped";s:10:"product_id";s:2:"10";}}s:20:"super_product_config";a:3:{s:12:"product_code";s:12:"product_type";s:12:"product_type";s:7:"grouped";s:10:"product_id";s:2:"10";}}', NULL, 1, 'Arcadio Gym Short', 'Arcadio Gym Short', NULL, NULL, NULL, 0, 0, NULL, '0.0000', '0.0000', '1.0000', '0.0000', '0.0000', NULL, '24.0000', '24.0000', '24.0000', '24.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '24.0000', '24.0000', '0.0000', '0.0000', '0.0000', NULL, NULL, NULL, NULL, NULL, '24.0000', '24.0000', '24.0000', '24.0000', '0.0000', '0.0000', NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, 0, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL),
(9, 4, NULL, 23, 1, '2016-04-28 03:06:22', '2016-04-28 03:06:22', 5, 'configurable', 'a:6:{s:15:"info_buyRequest";a:6:{s:4:"uenc";s:100:"aHR0cDovL2xvY2FsaG9zdC92ZXNfZmFzb255L3Byb2R1Y3QtY29uZmlndXJhdGlvbi1tYWdlbnRvLmh0bWw_b3B0aW9ucz1jYXJ0";s:7:"product";s:1:"5";s:28:"selected_configurable_option";s:1:"6";s:15:"related_product";s:0:"";s:15:"super_attribute";a:1:{i:90;s:1:"4";}s:3:"qty";s:1:"1";}s:15:"attributes_info";a:1:{i:0;a:2:{s:5:"label";s:5:"Color";s:5:"value";s:4:"blue";}}s:11:"simple_name";s:34:"product configuration magento-blue";s:10:"simple_sku";s:34:"product configuration magento-blue";s:20:"product_calculations";i:1;s:13:"shipment_type";i:0;}', NULL, 1, 'product configuration magento-blue', 'product configuration magento', NULL, NULL, NULL, 0, 0, NULL, '0.0000', '0.0000', '1.0000', '0.0000', '0.0000', NULL, '120.0000', '120.0000', '120.0000', '120.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '120.0000', '120.0000', '0.0000', '0.0000', '0.0000', NULL, NULL, NULL, NULL, NULL, '120.0000', '120.0000', '120.0000', '120.0000', '0.0000', '0.0000', NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, 0, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL),
(10, 4, 9, 24, 1, '2016-04-28 03:06:22', '2016-04-28 03:06:22', 6, 'virtual', 'a:1:{s:15:"info_buyRequest";a:6:{s:4:"uenc";s:100:"aHR0cDovL2xvY2FsaG9zdC92ZXNfZmFzb255L3Byb2R1Y3QtY29uZmlndXJhdGlvbi1tYWdlbnRvLmh0bWw_b3B0aW9ucz1jYXJ0";s:7:"product";s:1:"5";s:28:"selected_configurable_option";s:1:"6";s:15:"related_product";s:0:"";s:15:"super_attribute";a:1:{i:90;s:1:"4";}s:3:"qty";s:1:"1";}}', NULL, 1, 'product configuration magento-blue', 'product configuration magento-blue', NULL, NULL, NULL, 0, 0, NULL, '0.0000', '0.0000', '1.0000', '0.0000', '0.0000', NULL, '0.0000', '0.0000', '0.0000', NULL, '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', '0.0000', NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, 0, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL);

-- --------------------------------------------------------

--
-- Table structure for table `sales_order_payment`
--

CREATE TABLE `sales_order_payment` (
  `entity_id` int(10) UNSIGNED NOT NULL COMMENT 'Entity Id',
  `parent_id` int(10) UNSIGNED NOT NULL COMMENT 'Parent Id',
  `base_shipping_captured` decimal(12,4) DEFAULT NULL COMMENT 'Base Shipping Captured',
  `shipping_captured` decimal(12,4) DEFAULT NULL COMMENT 'Shipping Captured',
  `amount_refunded` decimal(12,4) DEFAULT NULL COMMENT 'Amount Refunded',
  `base_amount_paid` decimal(12,4) DEFAULT NULL COMMENT 'Base Amount Paid',
  `amount_canceled` decimal(12,4) DEFAULT NULL COMMENT 'Amount Canceled',
  `base_amount_authorized` decimal(12,4) DEFAULT NULL COMMENT 'Base Amount Authorized',
  `base_amount_paid_online` decimal(12,4) DEFAULT NULL COMMENT 'Base Amount Paid Online',
  `base_amount_refunded_online` decimal(12,4) DEFAULT NULL COMMENT 'Base Amount Refunded Online',
  `base_shipping_amount` decimal(12,4) DEFAULT NULL COMMENT 'Base Shipping Amount',
  `shipping_amount` decimal(12,4) DEFAULT NULL COMMENT 'Shipping Amount',
  `amount_paid` decimal(12,4) DEFAULT NULL COMMENT 'Amount Paid',
  `amount_authorized` decimal(12,4) DEFAULT NULL COMMENT 'Amount Authorized',
  `base_amount_ordered` decimal(12,4) DEFAULT NULL COMMENT 'Base Amount Ordered',
  `base_shipping_refunded` decimal(12,4) DEFAULT NULL COMMENT 'Base Shipping Refunded',
  `shipping_refunded` decimal(12,4) DEFAULT NULL COMMENT 'Shipping Refunded',
  `base_amount_refunded` decimal(12,4) DEFAULT NULL COMMENT 'Base Amount Refunded',
  `amount_ordered` decimal(12,4) DEFAULT NULL COMMENT 'Amount Ordered',
  `base_amount_canceled` decimal(12,4) DEFAULT NULL COMMENT 'Base Amount Canceled',
  `quote_payment_id` int(11) DEFAULT NULL COMMENT 'Quote Payment Id',
  `additional_data` text COMMENT 'Additional Data',
  `cc_exp_month` varchar(12) DEFAULT NULL COMMENT 'Cc Exp Month',
  `cc_ss_start_year` varchar(12) DEFAULT NULL COMMENT 'Cc Ss Start Year',
  `echeck_bank_name` varchar(128) DEFAULT NULL COMMENT 'Echeck Bank Name',
  `method` varchar(128) DEFAULT NULL COMMENT 'Method',
  `cc_debug_request_body` varchar(32) DEFAULT NULL COMMENT 'Cc Debug Request Body',
  `cc_secure_verify` varchar(32) DEFAULT NULL COMMENT 'Cc Secure Verify',
  `protection_eligibility` varchar(32) DEFAULT NULL COMMENT 'Protection Eligibility',
  `cc_approval` varchar(32) DEFAULT NULL COMMENT 'Cc Approval',
  `cc_last_4` varchar(100) DEFAULT NULL COMMENT 'Cc Last 4',
  `cc_status_description` varchar(32) DEFAULT NULL COMMENT 'Cc Status Description',
  `echeck_type` varchar(32) DEFAULT NULL COMMENT 'Echeck Type',
  `cc_debug_response_serialized` varchar(32) DEFAULT NULL COMMENT 'Cc Debug Response Serialized',
  `cc_ss_start_month` varchar(128) DEFAULT NULL COMMENT 'Cc Ss Start Month',
  `echeck_account_type` varchar(255) DEFAULT NULL COMMENT 'Echeck Account Type',
  `last_trans_id` varchar(32) DEFAULT NULL COMMENT 'Last Trans Id',
  `cc_cid_status` varchar(32) DEFAULT NULL COMMENT 'Cc Cid Status',
  `cc_owner` varchar(128) DEFAULT NULL COMMENT 'Cc Owner',
  `cc_type` varchar(32) DEFAULT NULL COMMENT 'Cc Type',
  `po_number` varchar(32) DEFAULT NULL COMMENT 'Po Number',
  `cc_exp_year` varchar(4) DEFAULT NULL COMMENT 'Cc Exp Year',
  `cc_status` varchar(4) DEFAULT NULL COMMENT 'Cc Status',
  `echeck_routing_number` varchar(32) DEFAULT NULL COMMENT 'Echeck Routing Number',
  `account_status` varchar(32) DEFAULT NULL COMMENT 'Account Status',
  `anet_trans_method` varchar(32) DEFAULT NULL COMMENT 'Anet Trans Method',
  `cc_debug_response_body` varchar(32) DEFAULT NULL COMMENT 'Cc Debug Response Body',
  `cc_ss_issue` varchar(32) DEFAULT NULL COMMENT 'Cc Ss Issue',
  `echeck_account_name` varchar(32) DEFAULT NULL COMMENT 'Echeck Account Name',
  `cc_avs_status` varchar(32) DEFAULT NULL COMMENT 'Cc Avs Status',
  `cc_number_enc` varchar(32) DEFAULT NULL COMMENT 'Cc Number Enc',
  `cc_trans_id` varchar(32) DEFAULT NULL COMMENT 'Cc Trans Id',
  `address_status` varchar(32) DEFAULT NULL COMMENT 'Address Status',
  `additional_information` text COMMENT 'Additional Information'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Sales Flat Order Payment';

--
-- Dumping data for table `sales_order_payment`
--

INSERT INTO `sales_order_payment` (`entity_id`, `parent_id`, `base_shipping_captured`, `shipping_captured`, `amount_refunded`, `base_amount_paid`, `amount_canceled`, `base_amount_authorized`, `base_amount_paid_online`, `base_amount_refunded_online`, `base_shipping_amount`, `shipping_amount`, `amount_paid`, `amount_authorized`, `base_amount_ordered`, `base_shipping_refunded`, `shipping_refunded`, `base_amount_refunded`, `amount_ordered`, `base_amount_canceled`, `quote_payment_id`, `additional_data`, `cc_exp_month`, `cc_ss_start_year`, `echeck_bank_name`, `method`, `cc_debug_request_body`, `cc_secure_verify`, `protection_eligibility`, `cc_approval`, `cc_last_4`, `cc_status_description`, `echeck_type`, `cc_debug_response_serialized`, `cc_ss_start_month`, `echeck_account_type`, `last_trans_id`, `cc_cid_status`, `cc_owner`, `cc_type`, `po_number`, `cc_exp_year`, `cc_status`, `echeck_routing_number`, `account_status`, `anet_trans_method`, `cc_debug_response_body`, `cc_ss_issue`, `echeck_account_name`, `cc_avs_status`, `cc_number_enc`, `cc_trans_id`, `address_status`, `additional_information`) VALUES
(1, 1, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, '0.0000', '0.0000', NULL, NULL, '120.0000', NULL, NULL, NULL, '120.0000', NULL, NULL, NULL, NULL, NULL, NULL, 'checkmo', NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, 'a:3:{s:12:"method_title";s:19:"Check / Money order";s:10:"payable_to";N;s:15:"mailing_address";N;}'),
(2, 2, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, '0.0000', '0.0000', NULL, NULL, '120.0000', NULL, NULL, NULL, '120.0000', NULL, NULL, NULL, NULL, NULL, NULL, 'checkmo', NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, 'a:3:{s:12:"method_title";s:19:"Check / Money order";s:10:"payable_to";N;s:15:"mailing_address";N;}'),
(3, 3, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, '0.0000', '0.0000', NULL, NULL, '49.0000', NULL, NULL, NULL, '49.0000', NULL, NULL, NULL, NULL, NULL, NULL, 'checkmo', NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, 'a:3:{s:12:"method_title";s:19:"Check / Money order";s:10:"payable_to";N;s:15:"mailing_address";N;}'),
(4, 4, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, '0.0000', '0.0000', NULL, NULL, '169.0000', NULL, NULL, NULL, '169.0000', NULL, NULL, NULL, NULL, NULL, NULL, 'checkmo', NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, 'a:3:{s:12:"method_title";s:19:"Check / Money order";s:10:"payable_to";N;s:15:"mailing_address";N;}');

-- --------------------------------------------------------

--
-- Table structure for table `sales_order_status`
--

CREATE TABLE `sales_order_status` (
  `status` varchar(32) NOT NULL COMMENT 'Status',
  `label` varchar(128) NOT NULL COMMENT 'Label'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Sales Order Status Table';

--
-- Dumping data for table `sales_order_status`
--

INSERT INTO `sales_order_status` (`status`, `label`) VALUES
('canceled', 'Canceled'),
('closed', 'Closed'),
('complete', 'Complete'),
('fraud', 'Suspected Fraud'),
('holded', 'On Hold'),
('payment_review', 'Payment Review'),
('paypal_canceled_reversal', 'PayPal Canceled Reversal'),
('paypal_reversed', 'PayPal Reversed'),
('pending', 'Pending'),
('pending_payment', 'Pending Payment'),
('pending_paypal', 'Pending PayPal'),
('processing', 'Processing');

-- --------------------------------------------------------

--
-- Table structure for table `sales_order_status_history`
--

CREATE TABLE `sales_order_status_history` (
  `entity_id` int(10) UNSIGNED NOT NULL COMMENT 'Entity Id',
  `parent_id` int(10) UNSIGNED NOT NULL COMMENT 'Parent Id',
  `is_customer_notified` int(11) DEFAULT NULL COMMENT 'Is Customer Notified',
  `is_visible_on_front` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Is Visible On Front',
  `comment` text COMMENT 'Comment',
  `status` varchar(32) DEFAULT NULL COMMENT 'Status',
  `created_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT 'Created At',
  `entity_name` varchar(32) DEFAULT NULL COMMENT 'Shows what entity history is bind to.'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Sales Flat Order Status History';

-- --------------------------------------------------------

--
-- Table structure for table `sales_order_status_label`
--

CREATE TABLE `sales_order_status_label` (
  `status` varchar(32) NOT NULL COMMENT 'Status',
  `store_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Store Id',
  `label` varchar(128) NOT NULL COMMENT 'Label'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Sales Order Status Label Table';

-- --------------------------------------------------------

--
-- Table structure for table `sales_order_status_state`
--

CREATE TABLE `sales_order_status_state` (
  `status` varchar(32) NOT NULL COMMENT 'Status',
  `state` varchar(32) NOT NULL COMMENT 'Label',
  `is_default` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Is Default',
  `visible_on_front` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Visible on front'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Sales Order Status Table';

--
-- Dumping data for table `sales_order_status_state`
--

INSERT INTO `sales_order_status_state` (`status`, `state`, `is_default`, `visible_on_front`) VALUES
('canceled', 'canceled', 1, 1),
('closed', 'closed', 1, 1),
('complete', 'complete', 1, 1),
('fraud', 'payment_review', 0, 1),
('fraud', 'processing', 0, 1),
('holded', 'holded', 1, 1),
('payment_review', 'payment_review', 1, 1),
('pending', 'new', 1, 1),
('pending_payment', 'pending_payment', 1, 0),
('processing', 'processing', 1, 1);

-- --------------------------------------------------------

--
-- Table structure for table `sales_order_tax`
--

CREATE TABLE `sales_order_tax` (
  `tax_id` int(10) UNSIGNED NOT NULL COMMENT 'Tax Id',
  `order_id` int(10) UNSIGNED NOT NULL COMMENT 'Order Id',
  `code` varchar(255) DEFAULT NULL COMMENT 'Code',
  `title` varchar(255) DEFAULT NULL COMMENT 'Title',
  `percent` decimal(12,4) DEFAULT NULL COMMENT 'Percent',
  `amount` decimal(12,4) DEFAULT NULL COMMENT 'Amount',
  `priority` int(11) NOT NULL COMMENT 'Priority',
  `position` int(11) NOT NULL COMMENT 'Position',
  `base_amount` decimal(12,4) DEFAULT NULL COMMENT 'Base Amount',
  `process` smallint(6) NOT NULL COMMENT 'Process',
  `base_real_amount` decimal(12,4) DEFAULT NULL COMMENT 'Base Real Amount'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Sales Order Tax Table';

-- --------------------------------------------------------

--
-- Table structure for table `sales_order_tax_item`
--

CREATE TABLE `sales_order_tax_item` (
  `tax_item_id` int(10) UNSIGNED NOT NULL COMMENT 'Tax Item Id',
  `tax_id` int(10) UNSIGNED NOT NULL COMMENT 'Tax Id',
  `item_id` int(10) UNSIGNED DEFAULT NULL COMMENT 'Item Id',
  `tax_percent` decimal(12,4) NOT NULL COMMENT 'Real Tax Percent For Item',
  `amount` decimal(12,4) NOT NULL COMMENT 'Tax amount for the item and tax rate',
  `base_amount` decimal(12,4) NOT NULL COMMENT 'Base tax amount for the item and tax rate',
  `real_amount` decimal(12,4) NOT NULL COMMENT 'Real tax amount for the item and tax rate',
  `real_base_amount` decimal(12,4) NOT NULL COMMENT 'Real base tax amount for the item and tax rate',
  `associated_item_id` int(10) UNSIGNED DEFAULT NULL COMMENT 'Id of the associated item',
  `taxable_item_type` varchar(32) NOT NULL COMMENT 'Type of the taxable item'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Sales Order Tax Item';

-- --------------------------------------------------------

--
-- Table structure for table `sales_payment_transaction`
--

CREATE TABLE `sales_payment_transaction` (
  `transaction_id` int(10) UNSIGNED NOT NULL COMMENT 'Transaction Id',
  `parent_id` int(10) UNSIGNED DEFAULT NULL COMMENT 'Parent Id',
  `order_id` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Order Id',
  `payment_id` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Payment Id',
  `txn_id` varchar(100) DEFAULT NULL COMMENT 'Txn Id',
  `parent_txn_id` varchar(100) DEFAULT NULL COMMENT 'Parent Txn Id',
  `txn_type` varchar(15) DEFAULT NULL COMMENT 'Txn Type',
  `is_closed` smallint(5) UNSIGNED NOT NULL DEFAULT '1' COMMENT 'Is Closed',
  `additional_information` blob COMMENT 'Additional Information',
  `created_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT 'Created At'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Sales Payment Transaction';

-- --------------------------------------------------------

--
-- Table structure for table `sales_refunded_aggregated`
--

CREATE TABLE `sales_refunded_aggregated` (
  `id` int(10) UNSIGNED NOT NULL COMMENT 'Id',
  `period` date DEFAULT NULL COMMENT 'Period',
  `store_id` smallint(5) UNSIGNED DEFAULT NULL COMMENT 'Store Id',
  `order_status` varchar(50) NOT NULL COMMENT 'Order Status',
  `orders_count` int(11) NOT NULL DEFAULT '0' COMMENT 'Orders Count',
  `refunded` decimal(12,4) DEFAULT NULL COMMENT 'Refunded',
  `online_refunded` decimal(12,4) DEFAULT NULL COMMENT 'Online Refunded',
  `offline_refunded` decimal(12,4) DEFAULT NULL COMMENT 'Offline Refunded'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Sales Refunded Aggregated';

-- --------------------------------------------------------

--
-- Table structure for table `sales_refunded_aggregated_order`
--

CREATE TABLE `sales_refunded_aggregated_order` (
  `id` int(10) UNSIGNED NOT NULL COMMENT 'Id',
  `period` date DEFAULT NULL COMMENT 'Period',
  `store_id` smallint(5) UNSIGNED DEFAULT NULL COMMENT 'Store Id',
  `order_status` varchar(50) DEFAULT NULL COMMENT 'Order Status',
  `orders_count` int(11) NOT NULL DEFAULT '0' COMMENT 'Orders Count',
  `refunded` decimal(12,4) DEFAULT NULL COMMENT 'Refunded',
  `online_refunded` decimal(12,4) DEFAULT NULL COMMENT 'Online Refunded',
  `offline_refunded` decimal(12,4) DEFAULT NULL COMMENT 'Offline Refunded'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Sales Refunded Aggregated Order';

-- --------------------------------------------------------

--
-- Table structure for table `sales_sequence_meta`
--

CREATE TABLE `sales_sequence_meta` (
  `meta_id` int(10) UNSIGNED NOT NULL COMMENT 'Id',
  `entity_type` varchar(32) NOT NULL COMMENT 'Prefix',
  `store_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Store Id',
  `sequence_table` varchar(32) NOT NULL COMMENT 'table for sequence'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='sales_sequence_meta';

--
-- Dumping data for table `sales_sequence_meta`
--

INSERT INTO `sales_sequence_meta` (`meta_id`, `entity_type`, `store_id`, `sequence_table`) VALUES
(1, 'order', 0, 'sequence_order_0'),
(2, 'invoice', 0, 'sequence_invoice_0'),
(3, 'creditmemo', 0, 'sequence_creditmemo_0'),
(4, 'shipment', 0, 'sequence_shipment_0'),
(5, 'order', 1, 'sequence_order_1'),
(6, 'invoice', 1, 'sequence_invoice_1'),
(7, 'creditmemo', 1, 'sequence_creditmemo_1'),
(8, 'shipment', 1, 'sequence_shipment_1'),
(9, 'order', 2, 'sequence_order_2'),
(10, 'invoice', 2, 'sequence_invoice_2'),
(11, 'creditmemo', 2, 'sequence_creditmemo_2'),
(12, 'shipment', 2, 'sequence_shipment_2');

-- --------------------------------------------------------

--
-- Table structure for table `sales_sequence_profile`
--

CREATE TABLE `sales_sequence_profile` (
  `profile_id` int(10) UNSIGNED NOT NULL COMMENT 'Id',
  `meta_id` int(10) UNSIGNED NOT NULL COMMENT 'Meta_id',
  `prefix` varchar(32) DEFAULT NULL COMMENT 'Prefix',
  `suffix` varchar(32) DEFAULT NULL COMMENT 'Suffix',
  `start_value` int(10) UNSIGNED NOT NULL DEFAULT '1' COMMENT 'Start value for sequence',
  `step` int(10) UNSIGNED NOT NULL DEFAULT '1' COMMENT 'Step for sequence',
  `max_value` int(10) UNSIGNED NOT NULL COMMENT 'MaxValue for sequence',
  `warning_value` int(10) UNSIGNED NOT NULL COMMENT 'WarningValue for sequence',
  `is_active` tinyint(1) NOT NULL DEFAULT '0' COMMENT 'isActive flag'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='sales_sequence_profile';

--
-- Dumping data for table `sales_sequence_profile`
--

INSERT INTO `sales_sequence_profile` (`profile_id`, `meta_id`, `prefix`, `suffix`, `start_value`, `step`, `max_value`, `warning_value`, `is_active`) VALUES
(1, 1, NULL, NULL, 1, 1, 0, 0, 1),
(2, 2, NULL, NULL, 1, 1, 0, 0, 1),
(3, 3, NULL, NULL, 1, 1, 0, 0, 1),
(4, 4, NULL, NULL, 1, 1, 0, 0, 1),
(5, 5, NULL, NULL, 1, 1, 0, 0, 1),
(6, 6, NULL, NULL, 1, 1, 0, 0, 1),
(7, 7, NULL, NULL, 1, 1, 0, 0, 1),
(8, 8, NULL, NULL, 1, 1, 0, 0, 1),
(9, 9, '2', NULL, 1, 1, 0, 0, 1),
(10, 10, '2', NULL, 1, 1, 0, 0, 1),
(11, 11, '2', NULL, 1, 1, 0, 0, 1),
(12, 12, '2', NULL, 1, 1, 0, 0, 1);

-- --------------------------------------------------------

--
-- Table structure for table `sales_shipment`
--

CREATE TABLE `sales_shipment` (
  `entity_id` int(10) UNSIGNED NOT NULL COMMENT 'Entity Id',
  `store_id` smallint(5) UNSIGNED DEFAULT NULL COMMENT 'Store Id',
  `total_weight` decimal(12,4) DEFAULT NULL COMMENT 'Total Weight',
  `total_qty` decimal(12,4) DEFAULT NULL COMMENT 'Total Qty',
  `email_sent` smallint(5) UNSIGNED DEFAULT NULL COMMENT 'Email Sent',
  `send_email` smallint(5) UNSIGNED DEFAULT NULL COMMENT 'Send Email',
  `order_id` int(10) UNSIGNED NOT NULL COMMENT 'Order Id',
  `customer_id` int(11) DEFAULT NULL COMMENT 'Customer Id',
  `shipping_address_id` int(11) DEFAULT NULL COMMENT 'Shipping Address Id',
  `billing_address_id` int(11) DEFAULT NULL COMMENT 'Billing Address Id',
  `shipment_status` int(11) DEFAULT NULL COMMENT 'Shipment Status',
  `increment_id` varchar(50) DEFAULT NULL COMMENT 'Increment Id',
  `created_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT 'Created At',
  `updated_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP COMMENT 'Updated At',
  `packages` text COMMENT 'Packed Products in Packages',
  `shipping_label` mediumblob COMMENT 'Shipping Label Content',
  `customer_note` text COMMENT 'Customer Note',
  `customer_note_notify` smallint(5) UNSIGNED DEFAULT NULL COMMENT 'Customer Note Notify'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Sales Flat Shipment';

-- --------------------------------------------------------

--
-- Table structure for table `sales_shipment_comment`
--

CREATE TABLE `sales_shipment_comment` (
  `entity_id` int(10) UNSIGNED NOT NULL COMMENT 'Entity Id',
  `parent_id` int(10) UNSIGNED NOT NULL COMMENT 'Parent Id',
  `is_customer_notified` int(11) DEFAULT NULL COMMENT 'Is Customer Notified',
  `is_visible_on_front` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Is Visible On Front',
  `comment` text COMMENT 'Comment',
  `created_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT 'Created At'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Sales Flat Shipment Comment';

-- --------------------------------------------------------

--
-- Table structure for table `sales_shipment_grid`
--

CREATE TABLE `sales_shipment_grid` (
  `entity_id` int(10) UNSIGNED NOT NULL COMMENT 'Entity Id',
  `increment_id` varchar(50) DEFAULT NULL COMMENT 'Increment Id',
  `store_id` smallint(5) UNSIGNED DEFAULT NULL COMMENT 'Store Id',
  `order_increment_id` varchar(32) NOT NULL COMMENT 'Order Increment Id',
  `order_id` int(10) UNSIGNED NOT NULL COMMENT 'Order Id',
  `order_created_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP COMMENT 'Order Increment Id',
  `customer_name` varchar(128) NOT NULL COMMENT 'Customer Name',
  `total_qty` decimal(12,4) DEFAULT NULL COMMENT 'Total Qty',
  `shipment_status` int(11) DEFAULT NULL COMMENT 'Shipment Status',
  `order_status` varchar(32) DEFAULT NULL COMMENT 'Order',
  `billing_address` varchar(255) DEFAULT NULL COMMENT 'Billing Address',
  `shipping_address` varchar(255) DEFAULT NULL COMMENT 'Shipping Address',
  `billing_name` varchar(128) DEFAULT NULL COMMENT 'Billing Name',
  `shipping_name` varchar(128) DEFAULT NULL COMMENT 'Shipping Name',
  `customer_email` varchar(128) DEFAULT NULL COMMENT 'Customer Email',
  `customer_group_id` smallint(6) DEFAULT NULL COMMENT 'Customer Group Id',
  `payment_method` varchar(32) DEFAULT NULL COMMENT 'Payment Method',
  `shipping_information` varchar(255) DEFAULT NULL COMMENT 'Shipping Method Name',
  `created_at` timestamp NULL DEFAULT NULL COMMENT 'Created At',
  `updated_at` timestamp NULL DEFAULT NULL COMMENT 'Updated At'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Sales Flat Shipment Grid';

-- --------------------------------------------------------

--
-- Table structure for table `sales_shipment_item`
--

CREATE TABLE `sales_shipment_item` (
  `entity_id` int(10) UNSIGNED NOT NULL COMMENT 'Entity Id',
  `parent_id` int(10) UNSIGNED NOT NULL COMMENT 'Parent Id',
  `row_total` decimal(12,4) DEFAULT NULL COMMENT 'Row Total',
  `price` decimal(12,4) DEFAULT NULL COMMENT 'Price',
  `weight` decimal(12,4) DEFAULT NULL COMMENT 'Weight',
  `qty` decimal(12,4) DEFAULT NULL COMMENT 'Qty',
  `product_id` int(11) DEFAULT NULL COMMENT 'Product Id',
  `order_item_id` int(11) DEFAULT NULL COMMENT 'Order Item Id',
  `additional_data` text COMMENT 'Additional Data',
  `description` text COMMENT 'Description',
  `name` varchar(255) DEFAULT NULL COMMENT 'Name',
  `sku` varchar(255) DEFAULT NULL COMMENT 'Sku'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Sales Flat Shipment Item';

-- --------------------------------------------------------

--
-- Table structure for table `sales_shipment_track`
--

CREATE TABLE `sales_shipment_track` (
  `entity_id` int(10) UNSIGNED NOT NULL COMMENT 'Entity Id',
  `parent_id` int(10) UNSIGNED NOT NULL COMMENT 'Parent Id',
  `weight` decimal(12,4) DEFAULT NULL COMMENT 'Weight',
  `qty` decimal(12,4) DEFAULT NULL COMMENT 'Qty',
  `order_id` int(10) UNSIGNED NOT NULL COMMENT 'Order Id',
  `track_number` text COMMENT 'Number',
  `description` text COMMENT 'Description',
  `title` varchar(255) DEFAULT NULL COMMENT 'Title',
  `carrier_code` varchar(32) DEFAULT NULL COMMENT 'Carrier Code',
  `created_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT 'Created At',
  `updated_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP COMMENT 'Updated At'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Sales Flat Shipment Track';

-- --------------------------------------------------------

--
-- Table structure for table `sales_shipping_aggregated`
--

CREATE TABLE `sales_shipping_aggregated` (
  `id` int(10) UNSIGNED NOT NULL COMMENT 'Id',
  `period` date DEFAULT NULL COMMENT 'Period',
  `store_id` smallint(5) UNSIGNED DEFAULT NULL COMMENT 'Store Id',
  `order_status` varchar(50) DEFAULT NULL COMMENT 'Order Status',
  `shipping_description` varchar(255) DEFAULT NULL COMMENT 'Shipping Description',
  `orders_count` int(11) NOT NULL DEFAULT '0' COMMENT 'Orders Count',
  `total_shipping` decimal(12,4) DEFAULT NULL COMMENT 'Total Shipping',
  `total_shipping_actual` decimal(12,4) DEFAULT NULL COMMENT 'Total Shipping Actual'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Sales Shipping Aggregated';

-- --------------------------------------------------------

--
-- Table structure for table `sales_shipping_aggregated_order`
--

CREATE TABLE `sales_shipping_aggregated_order` (
  `id` int(10) UNSIGNED NOT NULL COMMENT 'Id',
  `period` date DEFAULT NULL COMMENT 'Period',
  `store_id` smallint(5) UNSIGNED DEFAULT NULL COMMENT 'Store Id',
  `order_status` varchar(50) DEFAULT NULL COMMENT 'Order Status',
  `shipping_description` varchar(255) DEFAULT NULL COMMENT 'Shipping Description',
  `orders_count` int(11) NOT NULL DEFAULT '0' COMMENT 'Orders Count',
  `total_shipping` decimal(12,4) DEFAULT NULL COMMENT 'Total Shipping',
  `total_shipping_actual` decimal(12,4) DEFAULT NULL COMMENT 'Total Shipping Actual'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Sales Shipping Aggregated Order';

-- --------------------------------------------------------

--
-- Table structure for table `search_query`
--

CREATE TABLE `search_query` (
  `query_id` int(10) UNSIGNED NOT NULL COMMENT 'Query ID',
  `query_text` varchar(255) DEFAULT NULL COMMENT 'Query text',
  `num_results` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Num results',
  `popularity` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Popularity',
  `redirect` varchar(255) DEFAULT NULL COMMENT 'Redirect',
  `synonym_for` varchar(255) DEFAULT NULL COMMENT 'Synonym for',
  `store_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Store ID',
  `display_in_terms` smallint(6) NOT NULL DEFAULT '1' COMMENT 'Display in terms',
  `is_active` smallint(6) DEFAULT '1' COMMENT 'Active status',
  `is_processed` smallint(6) DEFAULT '0' COMMENT 'Processed status',
  `updated_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP COMMENT 'Updated at'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Search query table';

--
-- Dumping data for table `search_query`
--

INSERT INTO `search_query` (`query_id`, `query_text`, `num_results`, `popularity`, `redirect`, `synonym_for`, `store_id`, `display_in_terms`, `is_active`, `is_processed`, `updated_at`) VALUES
(1, 'l', 0, 1, NULL, NULL, 1, 1, 1, 0, '2016-04-21 07:43:20'),
(3, 'll', 0, 1, NULL, NULL, 1, 1, 1, 0, '2016-04-21 07:43:22'),
(5, 'll'';', 0, 2, NULL, NULL, 1, 1, 1, 0, '2016-04-21 07:43:28'),
(9, 'blue', 2, 1, NULL, NULL, 1, 1, 1, 0, '2016-04-21 07:43:50'),
(10, 'venustheme', 0, 2, NULL, NULL, 1, 1, 1, 0, '2016-04-27 08:17:48'),
(12, 'venustheme test', 0, 2, NULL, NULL, 1, 1, 1, 0, '2016-04-27 08:18:26'),
(14, 'venustheme demo', 0, 2, NULL, NULL, 1, 1, 1, 0, '2016-04-27 08:18:05'),
(22, 'Venustheme magento 2', 3, 1, NULL, NULL, 1, 1, 1, 0, '2016-04-27 08:20:16'),
(24, 'Venustheme  magento 2', 3, 2, NULL, NULL, 1, 1, 1, 0, '2016-04-27 08:23:52');

-- --------------------------------------------------------

--
-- Table structure for table `sendfriend_log`
--

CREATE TABLE `sendfriend_log` (
  `log_id` int(10) UNSIGNED NOT NULL COMMENT 'Log ID',
  `ip` bigint(20) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Customer IP address',
  `time` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Log time',
  `website_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Website ID'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Send to friend function log storage table';

-- --------------------------------------------------------

--
-- Table structure for table `sequence_creditmemo_0`
--

CREATE TABLE `sequence_creditmemo_0` (
  `sequence_value` int(10) UNSIGNED NOT NULL
) ENGINE=InnoDB DEFAULT CHARSET=latin1;

-- --------------------------------------------------------

--
-- Table structure for table `sequence_creditmemo_1`
--

CREATE TABLE `sequence_creditmemo_1` (
  `sequence_value` int(10) UNSIGNED NOT NULL
) ENGINE=InnoDB DEFAULT CHARSET=latin1;

-- --------------------------------------------------------

--
-- Table structure for table `sequence_creditmemo_2`
--

CREATE TABLE `sequence_creditmemo_2` (
  `sequence_value` int(10) UNSIGNED NOT NULL
) ENGINE=InnoDB DEFAULT CHARSET=latin1;

-- --------------------------------------------------------

--
-- Table structure for table `sequence_invoice_0`
--

CREATE TABLE `sequence_invoice_0` (
  `sequence_value` int(10) UNSIGNED NOT NULL
) ENGINE=InnoDB DEFAULT CHARSET=latin1;

-- --------------------------------------------------------

--
-- Table structure for table `sequence_invoice_1`
--

CREATE TABLE `sequence_invoice_1` (
  `sequence_value` int(10) UNSIGNED NOT NULL
) ENGINE=InnoDB DEFAULT CHARSET=latin1;

-- --------------------------------------------------------

--
-- Table structure for table `sequence_invoice_2`
--

CREATE TABLE `sequence_invoice_2` (
  `sequence_value` int(10) UNSIGNED NOT NULL
) ENGINE=InnoDB DEFAULT CHARSET=latin1;

-- --------------------------------------------------------

--
-- Table structure for table `sequence_order_0`
--

CREATE TABLE `sequence_order_0` (
  `sequence_value` int(10) UNSIGNED NOT NULL
) ENGINE=InnoDB DEFAULT CHARSET=latin1;

-- --------------------------------------------------------

--
-- Table structure for table `sequence_order_1`
--

CREATE TABLE `sequence_order_1` (
  `sequence_value` int(10) UNSIGNED NOT NULL
) ENGINE=InnoDB DEFAULT CHARSET=latin1;

--
-- Dumping data for table `sequence_order_1`
--

INSERT INTO `sequence_order_1` (`sequence_value`) VALUES
(1),
(2),
(3),
(4);

-- --------------------------------------------------------

--
-- Table structure for table `sequence_order_2`
--

CREATE TABLE `sequence_order_2` (
  `sequence_value` int(10) UNSIGNED NOT NULL
) ENGINE=InnoDB DEFAULT CHARSET=latin1;

-- --------------------------------------------------------

--
-- Table structure for table `sequence_shipment_0`
--

CREATE TABLE `sequence_shipment_0` (
  `sequence_value` int(10) UNSIGNED NOT NULL
) ENGINE=InnoDB DEFAULT CHARSET=latin1;

-- --------------------------------------------------------

--
-- Table structure for table `sequence_shipment_1`
--

CREATE TABLE `sequence_shipment_1` (
  `sequence_value` int(10) UNSIGNED NOT NULL
) ENGINE=InnoDB DEFAULT CHARSET=latin1;

-- --------------------------------------------------------

--
-- Table structure for table `sequence_shipment_2`
--

CREATE TABLE `sequence_shipment_2` (
  `sequence_value` int(10) UNSIGNED NOT NULL
) ENGINE=InnoDB DEFAULT CHARSET=latin1;

-- --------------------------------------------------------

--
-- Table structure for table `session`
--

CREATE TABLE `session` (
  `session_id` varchar(255) NOT NULL COMMENT 'Session Id',
  `session_expires` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Date of Session Expiration',
  `session_data` mediumblob NOT NULL COMMENT 'Session Data'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Database Sessions Storage';

-- --------------------------------------------------------

--
-- Table structure for table `setup_module`
--

CREATE TABLE `setup_module` (
  `module` varchar(50) NOT NULL COMMENT 'Module',
  `schema_version` varchar(50) DEFAULT NULL COMMENT 'Schema Version',
  `data_version` varchar(50) DEFAULT NULL COMMENT 'Data Version'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Module versions registry';

--
-- Dumping data for table `setup_module`
--

INSERT INTO `setup_module` (`module`, `schema_version`, `data_version`) VALUES
('Magento_AdminNotification', '2.0.0', '2.0.0'),
('Magento_AdvancedPricingImportExport', '2.0.0', '2.0.0'),
('Magento_Authorization', '2.0.0', '2.0.0'),
('Magento_Authorizenet', '2.0.0', '2.0.0'),
('Magento_Backend', '2.0.0', '2.0.0'),
('Magento_Backup', '2.0.0', '2.0.0'),
('Magento_Braintree', '2.0.0', '2.0.0'),
('Magento_Bundle', '2.0.1', '2.0.1'),
('Magento_BundleImportExport', '2.0.0', '2.0.0'),
('Magento_CacheInvalidate', '2.0.0', '2.0.0'),
('Magento_Captcha', '2.0.0', '2.0.0'),
('Magento_Catalog', '2.0.3', '2.0.3'),
('Magento_CatalogImportExport', '2.0.0', '2.0.0'),
('Magento_CatalogInventory', '2.0.0', '2.0.0'),
('Magento_CatalogRule', '2.0.0', '2.0.0'),
('Magento_CatalogRuleConfigurable', '2.0.0', '2.0.0'),
('Magento_CatalogSearch', '2.0.0', '2.0.0'),
('Magento_CatalogUrlRewrite', '2.0.0', '2.0.0'),
('Magento_CatalogWidget', '2.0.0', '2.0.0'),
('Magento_Checkout', '2.0.0', '2.0.0'),
('Magento_CheckoutAgreements', '2.0.1', '2.0.1'),
('Magento_Cms', '2.0.0', '2.0.0'),
('Magento_CmsUrlRewrite', '2.0.0', '2.0.0'),
('Magento_Config', '2.0.0', '2.0.0'),
('Magento_ConfigurableImportExport', '2.0.0', '2.0.0'),
('Magento_ConfigurableProduct', '2.0.0', '2.0.0'),
('Magento_Contact', '2.0.0', '2.0.0'),
('Magento_Cookie', '2.0.0', '2.0.0'),
('Magento_Cron', '2.0.0', '2.0.0'),
('Magento_CurrencySymbol', '2.0.0', '2.0.0'),
('Magento_Customer', '2.0.6', '2.0.6'),
('Magento_CustomerImportExport', '2.0.0', '2.0.0'),
('Magento_Deploy', '2.0.0', '2.0.0'),
('Magento_Developer', '2.0.0', '2.0.0'),
('Magento_Dhl', '2.0.0', '2.0.0'),
('Magento_Directory', '2.0.0', '2.0.0'),
('Magento_Downloadable', '2.0.0', '2.0.0'),
('Magento_DownloadableImportExport', '2.0.0', '2.0.0'),
('Magento_Eav', '2.0.0', '2.0.0'),
('Magento_Email', '2.0.0', '2.0.0'),
('Magento_EncryptionKey', '2.0.0', '2.0.0'),
('Magento_Fedex', '2.0.0', '2.0.0'),
('Magento_GiftMessage', '2.0.0', '2.0.0'),
('Magento_GoogleAdwords', '2.0.0', '2.0.0'),
('Magento_GoogleAnalytics', '2.0.0', '2.0.0'),
('Magento_GoogleOptimizer', '2.0.0', '2.0.0'),
('Magento_GroupedImportExport', '2.0.0', '2.0.0'),
('Magento_GroupedProduct', '2.0.0', '2.0.0'),
('Magento_ImportExport', '2.0.1', '2.0.1'),
('Magento_Indexer', '2.0.0', '2.0.0'),
('Magento_Integration', '2.0.1', '2.0.1'),
('Magento_LayeredNavigation', '2.0.0', '2.0.0'),
('Magento_Marketplace', '1.0.0', '1.0.0'),
('Magento_MediaStorage', '2.0.0', '2.0.0'),
('Magento_Msrp', '2.0.0', '2.0.0'),
('Magento_Multishipping', '2.0.0', '2.0.0'),
('Magento_NewRelicReporting', '2.0.0', '2.0.0'),
('Magento_Newsletter', '2.0.0', '2.0.0'),
('Magento_OfflinePayments', '2.0.0', '2.0.0'),
('Magento_OfflineShipping', '2.0.0', '2.0.0'),
('Magento_PageCache', '2.0.0', '2.0.0'),
('Magento_Payment', '2.0.0', '2.0.0'),
('Magento_Paypal', '2.0.0', '2.0.0'),
('Magento_Persistent', '2.0.0', '2.0.0'),
('Magento_ProductAlert', '2.0.0', '2.0.0'),
('Magento_ProductVideo', '2.0.0.2', '2.0.0.2'),
('Magento_Quote', '2.0.2', '2.0.2'),
('Magento_Reports', '2.0.0', '2.0.0'),
('Magento_RequireJs', '2.0.0', '2.0.0'),
('Magento_Review', '2.0.0', '2.0.0'),
('Magento_Rss', '2.0.0', '2.0.0'),
('Magento_Rule', '2.0.0', '2.0.0'),
('Magento_Sales', '2.0.1', '2.0.1'),
('Magento_SalesRule', '2.0.0', '2.0.0'),
('Magento_SalesSequence', '2.0.0', '2.0.0'),
('Magento_SampleData', '2.0.0', '2.0.0'),
('Magento_Search', '2.0.1', '2.0.1'),
('Magento_SendFriend', '2.0.0', '2.0.0'),
('Magento_Shipping', '2.0.0', '2.0.0'),
('Magento_Sitemap', '2.0.0', '2.0.0'),
('Magento_Store', '2.0.0', '2.0.0'),
('Magento_Swagger', '2.0.0', '2.0.0'),
('Magento_Swatches', '2.0.0', '2.0.0'),
('Magento_Tax', '2.0.1', '2.0.1'),
('Magento_TaxImportExport', '2.0.0', '2.0.0'),
('Magento_Theme', '2.0.0', '2.0.0'),
('Magento_Translation', '2.0.0', '2.0.0'),
('Magento_Ui', '2.0.0', '2.0.0'),
('Magento_Ups', '2.0.0', '2.0.0'),
('Magento_UrlRewrite', '2.0.0', '2.0.0'),
('Magento_User', '2.0.1', '2.0.1'),
('Magento_Usps', '2.0.0', '2.0.0'),
('Magento_Variable', '2.0.0', '2.0.0'),
('Magento_Version', '2.0.0', '2.0.0'),
('Magento_Webapi', '2.0.0', '2.0.0'),
('Magento_WebapiSecurity', '2.0.0', '2.0.0'),
('Magento_Weee', '2.0.0', '2.0.0'),
('Magento_Widget', '2.0.0', '2.0.0'),
('Magento_Wishlist', '2.0.0', '2.0.0');

-- --------------------------------------------------------

--
-- Table structure for table `shipping_tablerate`
--

CREATE TABLE `shipping_tablerate` (
  `pk` int(10) UNSIGNED NOT NULL COMMENT 'Primary key',
  `website_id` int(11) NOT NULL DEFAULT '0' COMMENT 'Website Id',
  `dest_country_id` varchar(4) NOT NULL DEFAULT '0' COMMENT 'Destination coutry ISO/2 or ISO/3 code',
  `dest_region_id` int(11) NOT NULL DEFAULT '0' COMMENT 'Destination Region Id',
  `dest_zip` varchar(10) NOT NULL DEFAULT '*' COMMENT 'Destination Post Code (Zip)',
  `condition_name` varchar(20) NOT NULL COMMENT 'Rate Condition name',
  `condition_value` decimal(12,4) NOT NULL DEFAULT '0.0000' COMMENT 'Rate condition value',
  `price` decimal(12,4) NOT NULL DEFAULT '0.0000' COMMENT 'Price',
  `cost` decimal(12,4) NOT NULL DEFAULT '0.0000' COMMENT 'Cost'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Shipping Tablerate';

-- --------------------------------------------------------

--
-- Table structure for table `sitemap`
--

CREATE TABLE `sitemap` (
  `sitemap_id` int(10) UNSIGNED NOT NULL COMMENT 'Sitemap Id',
  `sitemap_type` varchar(32) DEFAULT NULL COMMENT 'Sitemap Type',
  `sitemap_filename` varchar(32) DEFAULT NULL COMMENT 'Sitemap Filename',
  `sitemap_path` varchar(255) DEFAULT NULL COMMENT 'Sitemap Path',
  `sitemap_time` timestamp NULL DEFAULT NULL COMMENT 'Sitemap Time',
  `store_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Store id'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='XML Sitemap';

-- --------------------------------------------------------

--
-- Table structure for table `store`
--

CREATE TABLE `store` (
  `store_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Store Id',
  `code` varchar(32) DEFAULT NULL COMMENT 'Code',
  `website_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Website Id',
  `group_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Group Id',
  `name` varchar(255) NOT NULL COMMENT 'Store Name',
  `sort_order` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Store Sort Order',
  `is_active` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Store Activity'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Stores';

--
-- Dumping data for table `store`
--

INSERT INTO `store` (`store_id`, `code`, `website_id`, `group_id`, `name`, `sort_order`, `is_active`) VALUES
(0, 'admin', 0, 0, 'Admin', 0, 1),
(1, 'default', 1, 1, 'English', 0, 1),
(2, 'france', 1, 1, 'France', 2, 1);

-- --------------------------------------------------------

--
-- Table structure for table `store_group`
--

CREATE TABLE `store_group` (
  `group_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Group Id',
  `website_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Website Id',
  `name` varchar(255) NOT NULL COMMENT 'Store Group Name',
  `root_category_id` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Root Category Id',
  `default_store_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Default Store Id'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Store Groups';

--
-- Dumping data for table `store_group`
--

INSERT INTO `store_group` (`group_id`, `website_id`, `name`, `root_category_id`, `default_store_id`) VALUES
(0, 0, 'Default', 0, 0),
(1, 1, 'Main Website Store', 2, 1);

-- --------------------------------------------------------

--
-- Table structure for table `store_website`
--

CREATE TABLE `store_website` (
  `website_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Website Id',
  `code` varchar(32) DEFAULT NULL COMMENT 'Code',
  `name` varchar(64) DEFAULT NULL COMMENT 'Website Name',
  `sort_order` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Sort Order',
  `default_group_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Default Group Id',
  `is_default` smallint(5) UNSIGNED DEFAULT '0' COMMENT 'Defines Is Website Default'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Websites';

--
-- Dumping data for table `store_website`
--

INSERT INTO `store_website` (`website_id`, `code`, `name`, `sort_order`, `default_group_id`, `is_default`) VALUES
(0, 'admin', 'Admin', 0, 0, 0),
(1, 'base', 'Main Website', 0, 1, 1);

-- --------------------------------------------------------

--
-- Table structure for table `tax_calculation`
--

CREATE TABLE `tax_calculation` (
  `tax_calculation_id` int(11) NOT NULL COMMENT 'Tax Calculation Id',
  `tax_calculation_rate_id` int(11) NOT NULL COMMENT 'Tax Calculation Rate Id',
  `tax_calculation_rule_id` int(11) NOT NULL COMMENT 'Tax Calculation Rule Id',
  `customer_tax_class_id` smallint(6) NOT NULL COMMENT 'Customer Tax Class Id',
  `product_tax_class_id` smallint(6) NOT NULL COMMENT 'Product Tax Class Id'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Tax Calculation';

-- --------------------------------------------------------

--
-- Table structure for table `tax_calculation_rate`
--

CREATE TABLE `tax_calculation_rate` (
  `tax_calculation_rate_id` int(11) NOT NULL COMMENT 'Tax Calculation Rate Id',
  `tax_country_id` varchar(2) NOT NULL COMMENT 'Tax Country Id',
  `tax_region_id` int(11) NOT NULL COMMENT 'Tax Region Id',
  `tax_postcode` varchar(21) DEFAULT NULL COMMENT 'Tax Postcode',
  `code` varchar(255) NOT NULL COMMENT 'Code',
  `rate` decimal(12,4) NOT NULL COMMENT 'Rate',
  `zip_is_range` smallint(6) DEFAULT NULL COMMENT 'Zip Is Range',
  `zip_from` int(10) UNSIGNED DEFAULT NULL COMMENT 'Zip From',
  `zip_to` int(10) UNSIGNED DEFAULT NULL COMMENT 'Zip To'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Tax Calculation Rate';

--
-- Dumping data for table `tax_calculation_rate`
--

INSERT INTO `tax_calculation_rate` (`tax_calculation_rate_id`, `tax_country_id`, `tax_region_id`, `tax_postcode`, `code`, `rate`, `zip_is_range`, `zip_from`, `zip_to`) VALUES
(1, 'US', 12, '*', 'US-CA-*-Rate 1', '8.2500', NULL, NULL, NULL),
(2, 'US', 43, '*', 'US-NY-*-Rate 1', '8.3750', NULL, NULL, NULL);

-- --------------------------------------------------------

--
-- Table structure for table `tax_calculation_rate_title`
--

CREATE TABLE `tax_calculation_rate_title` (
  `tax_calculation_rate_title_id` int(11) NOT NULL COMMENT 'Tax Calculation Rate Title Id',
  `tax_calculation_rate_id` int(11) NOT NULL COMMENT 'Tax Calculation Rate Id',
  `store_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Store Id',
  `value` varchar(255) NOT NULL COMMENT 'Value'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Tax Calculation Rate Title';

-- --------------------------------------------------------

--
-- Table structure for table `tax_calculation_rule`
--

CREATE TABLE `tax_calculation_rule` (
  `tax_calculation_rule_id` int(11) NOT NULL COMMENT 'Tax Calculation Rule Id',
  `code` varchar(255) NOT NULL COMMENT 'Code',
  `priority` int(11) NOT NULL COMMENT 'Priority',
  `position` int(11) NOT NULL COMMENT 'Position',
  `calculate_subtotal` int(11) NOT NULL COMMENT 'Calculate off subtotal option'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Tax Calculation Rule';

-- --------------------------------------------------------

--
-- Table structure for table `tax_class`
--

CREATE TABLE `tax_class` (
  `class_id` smallint(6) NOT NULL COMMENT 'Class Id',
  `class_name` varchar(255) NOT NULL COMMENT 'Class Name',
  `class_type` varchar(8) NOT NULL DEFAULT 'CUSTOMER' COMMENT 'Class Type'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Tax Class';

--
-- Dumping data for table `tax_class`
--

INSERT INTO `tax_class` (`class_id`, `class_name`, `class_type`) VALUES
(2, 'Taxable Goods', 'PRODUCT'),
(3, 'Retail Customer', 'CUSTOMER');

-- --------------------------------------------------------

--
-- Table structure for table `tax_order_aggregated_created`
--

CREATE TABLE `tax_order_aggregated_created` (
  `id` int(10) UNSIGNED NOT NULL COMMENT 'Id',
  `period` date DEFAULT NULL COMMENT 'Period',
  `store_id` smallint(5) UNSIGNED DEFAULT NULL COMMENT 'Store Id',
  `code` varchar(255) NOT NULL COMMENT 'Code',
  `order_status` varchar(50) NOT NULL COMMENT 'Order Status',
  `percent` float DEFAULT NULL COMMENT 'Percent',
  `orders_count` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Orders Count',
  `tax_base_amount_sum` float DEFAULT NULL COMMENT 'Tax Base Amount Sum'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Tax Order Aggregation';

-- --------------------------------------------------------

--
-- Table structure for table `tax_order_aggregated_updated`
--

CREATE TABLE `tax_order_aggregated_updated` (
  `id` int(10) UNSIGNED NOT NULL COMMENT 'Id',
  `period` date DEFAULT NULL COMMENT 'Period',
  `store_id` smallint(5) UNSIGNED DEFAULT NULL COMMENT 'Store Id',
  `code` varchar(255) NOT NULL COMMENT 'Code',
  `order_status` varchar(50) NOT NULL COMMENT 'Order Status',
  `percent` float DEFAULT NULL COMMENT 'Percent',
  `orders_count` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Orders Count',
  `tax_base_amount_sum` float DEFAULT NULL COMMENT 'Tax Base Amount Sum'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Tax Order Aggregated Updated';

-- --------------------------------------------------------

--
-- Table structure for table `theme`
--

CREATE TABLE `theme` (
  `theme_id` int(10) UNSIGNED NOT NULL COMMENT 'Theme identifier',
  `parent_id` int(11) DEFAULT NULL COMMENT 'Parent Id',
  `theme_path` varchar(255) DEFAULT NULL COMMENT 'Theme Path',
  `theme_title` varchar(255) NOT NULL COMMENT 'Theme Title',
  `preview_image` varchar(255) DEFAULT NULL COMMENT 'Preview Image',
  `is_featured` tinyint(1) NOT NULL DEFAULT '0' COMMENT 'Is Theme Featured',
  `area` varchar(255) NOT NULL COMMENT 'Theme Area',
  `type` smallint(6) NOT NULL COMMENT 'Theme type: 0:physical, 1:virtual, 2:staging',
  `code` text COMMENT 'Full theme code, including package'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Core theme';

--
-- Dumping data for table `theme`
--

INSERT INTO `theme` (`theme_id`, `parent_id`, `theme_path`, `theme_title`, `preview_image`, `is_featured`, `area`, `type`, `code`) VALUES
(1, NULL, 'Magento/blank', 'Magento Blank', 'preview_image_570d02fbb60d7.jpeg', 0, 'frontend', 0, 'Magento/blank'),
(2, 1, 'Magento/luma', 'Magento Luma', 'preview_image_570d02fc409b7.jpeg', 0, 'frontend', 0, 'Magento/luma'),
(3, NULL, 'Magento/backend', 'Magento 2 backend', NULL, 0, 'adminhtml', 0, 'Magento/backend'),
(4, 1, 'Venustheme/fasony', 'Venustheme - Fasony', 'preview_image_570d0a2c6305d.jpeg', 0, 'frontend', 0, 'Venustheme/fasony');

-- --------------------------------------------------------

--
-- Table structure for table `theme_file`
--

CREATE TABLE `theme_file` (
  `theme_files_id` int(10) UNSIGNED NOT NULL COMMENT 'Theme files identifier',
  `theme_id` int(10) UNSIGNED NOT NULL COMMENT 'Theme Id',
  `file_path` varchar(255) DEFAULT NULL COMMENT 'Relative path to file',
  `file_type` varchar(32) NOT NULL COMMENT 'File Type',
  `content` longtext NOT NULL COMMENT 'File Content',
  `sort_order` smallint(6) NOT NULL DEFAULT '0' COMMENT 'Sort Order',
  `is_temporary` tinyint(1) NOT NULL DEFAULT '0' COMMENT 'Is Temporary File'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Core theme files';

-- --------------------------------------------------------

--
-- Table structure for table `translation`
--

CREATE TABLE `translation` (
  `key_id` int(10) UNSIGNED NOT NULL COMMENT 'Key Id of Translation',
  `string` varchar(255) NOT NULL DEFAULT 'Translate String' COMMENT 'Translation String',
  `store_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Store Id',
  `translate` varchar(255) DEFAULT NULL COMMENT 'Translate',
  `locale` varchar(20) NOT NULL DEFAULT 'en_US' COMMENT 'Locale',
  `crc_string` bigint(20) NOT NULL DEFAULT '1591228201' COMMENT 'Translation String CRC32 Hash'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Translations';

-- --------------------------------------------------------

--
-- Table structure for table `ui_bookmark`
--

CREATE TABLE `ui_bookmark` (
  `bookmark_id` int(10) UNSIGNED NOT NULL COMMENT 'Bookmark identifier',
  `user_id` int(10) UNSIGNED NOT NULL COMMENT 'User Id',
  `namespace` varchar(255) NOT NULL COMMENT 'Bookmark namespace',
  `identifier` varchar(255) NOT NULL COMMENT 'Bookmark Identifier',
  `current` smallint(6) NOT NULL COMMENT 'Mark current bookmark per user and identifier',
  `title` varchar(255) DEFAULT NULL COMMENT 'Bookmark title',
  `config` longtext COMMENT 'Bookmark config',
  `created_at` datetime NOT NULL COMMENT 'Bookmark created at',
  `updated_at` datetime NOT NULL COMMENT 'Bookmark updated at'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Bookmark';

--
-- Dumping data for table `ui_bookmark`
--

INSERT INTO `ui_bookmark` (`bookmark_id`, `user_id`, `namespace`, `identifier`, `current`, `title`, `config`, `created_at`, `updated_at`) VALUES
(1, 1, 'cms_block_listing', 'current', 0, NULL, '{"current":{"filters":{"applied":{"placeholder":true}},"search":{"value":""},"columns":{"block_id":{"visible":true,"sorting":"asc"},"title":{"visible":true,"sorting":false},"identifier":{"visible":true,"sorting":false},"store_id":{"visible":true,"sorting":false},"is_active":{"visible":true,"sorting":false},"ids":{"visible":true,"sorting":false},"actions":{"visible":true,"sorting":false},"creation_time":{"visible":true,"sorting":false},"update_time":{"visible":true,"sorting":false}},"paging":{"options":{"20":{"value":20,"label":20},"30":{"value":30,"label":30},"50":{"value":50,"label":50},"100":{"value":100,"label":100},"200":{"value":200,"label":200}},"value":20},"positions":{"ids":0,"block_id":1,"title":2,"identifier":3,"store_id":4,"is_active":5,"creation_time":6,"update_time":7,"actions":8}}}', '1970-01-01 00:00:00', '1970-01-01 00:00:00'),
(2, 1, 'cms_block_listing', 'default', 1, 'Default View', '{"views":{"default":{"label":"Default View","index":"default","editable":false,"data":{"filters":{"applied":{"placeholder":true}},"search":{"value":""},"columns":{"block_id":{"visible":true,"sorting":"asc"},"title":{"visible":true,"sorting":false},"identifier":{"visible":true,"sorting":false},"store_id":{"visible":true,"sorting":false},"is_active":{"visible":true,"sorting":false},"ids":{"visible":true,"sorting":false},"actions":{"visible":true,"sorting":false},"creation_time":{"visible":true,"sorting":false},"update_time":{"visible":true,"sorting":false}},"paging":{"options":{"20":{"value":20,"label":20},"30":{"value":30,"label":30},"50":{"value":50,"label":50},"100":{"value":100,"label":100},"200":{"value":200,"label":200}},"value":20},"positions":{"ids":0,"block_id":1,"title":2,"identifier":3,"store_id":4,"is_active":5,"creation_time":6,"update_time":7,"actions":8}},"value":"Default View"}}}', '1970-01-01 00:00:00', '1970-01-01 00:00:00'),
(3, 1, 'cms_page_listing', 'current', 0, NULL, '{"current":{"filters":{"applied":{"placeholder":true}},"search":{"value":""},"columns":{"page_id":{"visible":true,"sorting":"asc"},"title":{"visible":true,"sorting":false},"identifier":{"visible":true,"sorting":false},"store_id":{"visible":true,"sorting":false},"meta_keywords":{"visible":false,"sorting":false},"meta_description":{"visible":false,"sorting":false},"ids":{"visible":true,"sorting":false},"actions":{"visible":true,"sorting":false},"page_layout":{"visible":true,"sorting":false},"is_active":{"visible":true,"sorting":false},"custom_theme":{"visible":false,"sorting":false},"custom_root_template":{"visible":false,"sorting":false},"creation_time":{"visible":true,"sorting":false},"update_time":{"visible":true,"sorting":false},"custom_theme_from":{"visible":false,"sorting":false},"custom_theme_to":{"visible":false,"sorting":false}},"paging":{"options":{"20":{"value":20,"label":20},"30":{"value":30,"label":30},"50":{"value":50,"label":50},"100":{"value":100,"label":100},"200":{"value":200,"label":200}},"value":20},"positions":{"ids":0,"page_id":1,"title":2,"identifier":3,"page_layout":4,"store_id":5,"is_active":6,"creation_time":7,"update_time":8,"custom_theme_from":9,"custom_theme_to":10,"custom_theme":11,"custom_root_template":12,"meta_keywords":13,"meta_description":14,"actions":15}}}', '1970-01-01 00:00:00', '1970-01-01 00:00:00'),
(4, 1, 'cms_page_listing', 'default', 1, 'Default View', '{"views":{"default":{"label":"Default View","index":"default","editable":false,"data":{"filters":{"applied":{"placeholder":true}},"search":{"value":""},"columns":{"page_id":{"visible":true,"sorting":"asc"},"title":{"visible":true,"sorting":false},"identifier":{"visible":true,"sorting":false},"store_id":{"visible":true,"sorting":false},"meta_keywords":{"visible":false,"sorting":false},"meta_description":{"visible":false,"sorting":false},"ids":{"visible":true,"sorting":false},"actions":{"visible":true,"sorting":false},"page_layout":{"visible":true,"sorting":false},"is_active":{"visible":true,"sorting":false},"custom_theme":{"visible":false,"sorting":false},"custom_root_template":{"visible":false,"sorting":false},"creation_time":{"visible":true,"sorting":false},"update_time":{"visible":true,"sorting":false},"custom_theme_from":{"visible":false,"sorting":false},"custom_theme_to":{"visible":false,"sorting":false}},"paging":{"options":{"20":{"value":20,"label":20},"30":{"value":30,"label":30},"50":{"value":50,"label":50},"100":{"value":100,"label":100},"200":{"value":200,"label":200}},"value":20},"positions":{"ids":0,"page_id":1,"title":2,"identifier":3,"page_layout":4,"store_id":5,"is_active":6,"creation_time":7,"update_time":8,"custom_theme_from":9,"custom_theme_to":10,"custom_theme":11,"custom_root_template":12,"meta_keywords":13,"meta_description":14,"actions":15}},"value":"Default View"}}}', '1970-01-01 00:00:00', '1970-01-01 00:00:00'),
(5, 1, 'product_listing', 'current', 0, NULL, '{"current":{"filters":{"applied":{"placeholder":true}},"columns":{"entity_id":{"visible":true,"sorting":"asc"},"name":{"visible":true,"sorting":false},"sku":{"visible":true,"sorting":false},"price":{"visible":true,"sorting":false},"qty":{"visible":true,"sorting":false},"short_description":{"visible":false,"sorting":false},"special_price":{"visible":false,"sorting":false},"cost":{"visible":false,"sorting":false},"weight":{"visible":false,"sorting":false},"meta_title":{"visible":false,"sorting":false},"meta_keyword":{"visible":false,"sorting":false},"meta_description":{"visible":false,"sorting":false},"url_key":{"visible":false,"sorting":false},"msrp":{"visible":false,"sorting":false},"ids":{"visible":true,"sorting":false},"thumbnail":{"visible":true,"sorting":false},"type_id":{"visible":true,"sorting":false},"attribute_set_id":{"visible":true,"sorting":false},"visibility":{"visible":true,"sorting":false},"status":{"visible":true,"sorting":false},"websites":{"visible":true,"sorting":false},"custom_design":{"visible":false,"sorting":false},"page_layout":{"visible":false,"sorting":false},"country_of_manufacture":{"visible":false,"sorting":false},"tax_class_id":{"visible":false,"sorting":false},"gift_message_available":{"visible":false,"sorting":false},"actions":{"visible":true,"sorting":false},"special_from_date":{"visible":false,"sorting":false},"special_to_date":{"visible":false,"sorting":false},"news_from_date":{"visible":false,"sorting":false},"news_to_date":{"visible":false,"sorting":false},"custom_design_from":{"visible":false,"sorting":false},"custom_design_to":{"visible":false,"sorting":false},"color":{"visible":false,"sorting":false}},"paging":{"options":{"20":{"value":20,"label":20},"30":{"value":30,"label":30},"50":{"value":50,"label":50},"100":{"value":100,"label":100},"200":{"value":200,"label":200}},"value":20},"positions":{"ids":0,"entity_id":1,"thumbnail":2,"name":3,"type_id":4,"attribute_set_id":5,"sku":6,"price":7,"qty":8,"visibility":9,"status":10,"websites":11,"short_description":12,"special_price":13,"special_from_date":14,"special_to_date":15,"cost":16,"weight":17,"meta_title":18,"meta_keyword":19,"meta_description":20,"news_from_date":21,"news_to_date":22,"custom_design":23,"custom_design_from":24,"custom_design_to":25,"page_layout":26,"country_of_manufacture":27,"url_key":28,"msrp":29,"tax_class_id":30,"gift_message_available":31,"actions":32,"color":33}}}', '1970-01-01 00:00:00', '1970-01-01 00:00:00'),
(6, 1, 'product_listing', 'default', 1, 'Default View', '{"views":{"default":{"label":"Default View","index":"default","editable":false,"data":{"filters":{"applied":{"placeholder":true}},"columns":{"entity_id":{"visible":true,"sorting":"asc"},"name":{"visible":true,"sorting":false},"sku":{"visible":true,"sorting":false},"price":{"visible":true,"sorting":false},"qty":{"visible":true,"sorting":false},"short_description":{"visible":false,"sorting":false},"special_price":{"visible":false,"sorting":false},"cost":{"visible":false,"sorting":false},"weight":{"visible":false,"sorting":false},"meta_title":{"visible":false,"sorting":false},"meta_keyword":{"visible":false,"sorting":false},"meta_description":{"visible":false,"sorting":false},"url_key":{"visible":false,"sorting":false},"msrp":{"visible":false,"sorting":false},"ids":{"visible":true,"sorting":false},"thumbnail":{"visible":true,"sorting":false},"type_id":{"visible":true,"sorting":false},"attribute_set_id":{"visible":true,"sorting":false},"visibility":{"visible":true,"sorting":false},"status":{"visible":true,"sorting":false},"websites":{"visible":true,"sorting":false},"custom_design":{"visible":false,"sorting":false},"page_layout":{"visible":false,"sorting":false},"country_of_manufacture":{"visible":false,"sorting":false},"tax_class_id":{"visible":false,"sorting":false},"gift_message_available":{"visible":false,"sorting":false},"actions":{"visible":true,"sorting":false},"special_from_date":{"visible":false,"sorting":false},"special_to_date":{"visible":false,"sorting":false},"news_from_date":{"visible":false,"sorting":false},"news_to_date":{"visible":false,"sorting":false},"custom_design_from":{"visible":false,"sorting":false},"custom_design_to":{"visible":false,"sorting":false}},"paging":{"options":{"20":{"value":20,"label":20},"30":{"value":30,"label":30},"50":{"value":50,"label":50},"100":{"value":100,"label":100},"200":{"value":200,"label":200}},"value":20},"positions":{"ids":0,"entity_id":1,"thumbnail":2,"name":3,"type_id":4,"attribute_set_id":5,"sku":6,"price":7,"qty":8,"visibility":9,"status":10,"websites":11,"short_description":12,"special_price":13,"special_from_date":14,"special_to_date":15,"cost":16,"weight":17,"meta_title":18,"meta_keyword":19,"meta_description":20,"news_from_date":21,"news_to_date":22,"custom_design":23,"custom_design_from":24,"custom_design_to":25,"page_layout":26,"country_of_manufacture":27,"url_key":28,"msrp":29,"tax_class_id":30,"gift_message_available":31,"actions":32}},"value":"Default View"}}}', '1970-01-01 00:00:00', '1970-01-01 00:00:00'),
(7, 1, 'product_attributes_listing', 'current', 0, NULL, '{"current":{"filters":{"applied":{"placeholder":true}},"columns":{"attribute_code":{"visible":true,"sorting":"asc"},"frontend_label":{"visible":true,"sorting":false},"is_filterable":{"visible":true,"sorting":false},"is_required":{"visible":true,"sorting":false},"is_user_defined":{"visible":true,"sorting":false},"is_visible":{"visible":true,"sorting":false},"is_global":{"visible":true,"sorting":false},"is_searchable":{"visible":true,"sorting":false},"is_comparable":{"visible":true,"sorting":false},"ids":{"visible":true,"sorting":false}},"positions":{"ids":0,"is_filterable":1,"attribute_code":2,"frontend_label":3,"is_required":4,"is_user_defined":5,"is_visible":6,"is_global":7,"is_searchable":8,"is_comparable":9},"paging":{"options":{"20":{"value":20,"label":20},"30":{"value":30,"label":30},"50":{"value":50,"label":50},"100":{"value":100,"label":100},"200":{"value":200,"label":200}},"value":20}}}', '1970-01-01 00:00:00', '1970-01-01 00:00:00'),
(8, 1, 'product_attributes_listing', 'default', 1, 'Default View', '{"views":{"default":{"label":"Default View","index":"default","editable":false,"data":{"filters":{"applied":{"placeholder":true}},"columns":{"attribute_code":{"visible":true,"sorting":"asc"},"frontend_label":{"visible":true,"sorting":false},"is_filterable":{"visible":true,"sorting":false},"is_required":{"visible":true,"sorting":false},"is_user_defined":{"visible":true,"sorting":false},"is_visible":{"visible":true,"sorting":false},"is_global":{"visible":true,"sorting":false},"is_searchable":{"visible":true,"sorting":false},"is_comparable":{"visible":true,"sorting":false},"ids":{"visible":true,"sorting":false}},"positions":{"ids":0,"is_filterable":1,"attribute_code":2,"frontend_label":3,"is_required":4,"is_user_defined":5,"is_visible":6,"is_global":7,"is_searchable":8,"is_comparable":9},"paging":{"options":{"20":{"value":20,"label":20},"30":{"value":30,"label":30},"50":{"value":50,"label":50},"100":{"value":100,"label":100},"200":{"value":200,"label":200}},"value":20}},"value":"Default View"}}}', '1970-01-01 00:00:00', '1970-01-01 00:00:00');

-- --------------------------------------------------------

--
-- Table structure for table `url_rewrite`
--

CREATE TABLE `url_rewrite` (
  `url_rewrite_id` int(10) UNSIGNED NOT NULL COMMENT 'Rewrite Id',
  `entity_type` varchar(32) NOT NULL COMMENT 'Entity type code',
  `entity_id` int(10) UNSIGNED NOT NULL COMMENT 'Entity ID',
  `request_path` varchar(255) DEFAULT NULL COMMENT 'Request Path',
  `target_path` varchar(255) DEFAULT NULL COMMENT 'Target Path',
  `redirect_type` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Redirect Type',
  `store_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Store Id',
  `description` varchar(255) DEFAULT NULL COMMENT 'Description',
  `is_autogenerated` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Is rewrite generated automatically flag',
  `metadata` varchar(255) DEFAULT NULL COMMENT 'Meta data for url rewrite'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Url Rewrites';

--
-- Dumping data for table `url_rewrite`
--

INSERT INTO `url_rewrite` (`url_rewrite_id`, `entity_type`, `entity_id`, `request_path`, `target_path`, `redirect_type`, `store_id`, `description`, `is_autogenerated`, `metadata`) VALUES
(1, 'cms-page', 1, 'no-route', 'cms/page/view/page_id/1', 0, 1, NULL, 1, NULL),
(2, 'cms-page', 2, 'home', 'cms/page/view/page_id/2', 0, 1, NULL, 1, NULL),
(3, 'cms-page', 3, 'enable-cookies', 'cms/page/view/page_id/3', 0, 1, NULL, 1, NULL),
(4, 'cms-page', 4, 'privacy-policy-cookie-restriction-mode', 'cms/page/view/page_id/4', 0, 1, NULL, 1, NULL),
(5, 'category', 3, 'women.html', 'catalog/category/view/id/3', 0, 1, NULL, 1, NULL),
(7, 'category', 4, 'mens.html', 'catalog/category/view/id/4', 0, 1, NULL, 1, NULL),
(8, 'category', 4, 'women/mens.html', 'mens.html', 301, 1, NULL, 0, NULL),
(10, 'category', 5, 'accessories.html', 'catalog/category/view/id/5', 0, 1, NULL, 1, NULL),
(11, 'category', 5, 'mens/accessories.html', 'accessories.html', 301, 1, NULL, 0, NULL),
(12, 'category', 3, 'women.html', 'catalog/category/view/id/3', 0, 2, NULL, 1, NULL),
(13, 'category', 4, 'mens.html', 'catalog/category/view/id/4', 0, 2, NULL, 1, NULL),
(14, 'category', 5, 'accessories.html', 'catalog/category/view/id/5', 0, 2, NULL, 1, NULL),
(21, 'product', 1, 'ariel-roll-sleeve-sweatshirt.html', 'catalog/product/view/id/1', 0, 1, NULL, 1, NULL),
(22, 'product', 1, 'women/ariel-roll-sleeve-sweatshirt.html', 'catalog/product/view/id/1/category/3', 0, 1, NULL, 1, 'a:1:{s:11:"category_id";s:1:"3";}'),
(23, 'product', 1, 'mens/ariel-roll-sleeve-sweatshirt.html', 'catalog/product/view/id/1/category/4', 0, 1, NULL, 1, 'a:1:{s:11:"category_id";s:1:"4";}'),
(24, 'product', 1, 'accessories/ariel-roll-sleeve-sweatshirt.html', 'catalog/product/view/id/1/category/5', 0, 1, NULL, 1, 'a:1:{s:11:"category_id";s:1:"5";}'),
(25, 'product', 1, 'ariel-roll-sleeve-sweatshirt.html', 'catalog/product/view/id/1', 0, 2, NULL, 1, NULL),
(26, 'product', 1, 'women/ariel-roll-sleeve-sweatshirt.html', 'catalog/product/view/id/1/category/3', 0, 2, NULL, 1, 'a:1:{s:11:"category_id";s:1:"3";}'),
(27, 'product', 1, 'mens/ariel-roll-sleeve-sweatshirt.html', 'catalog/product/view/id/1/category/4', 0, 2, NULL, 1, 'a:1:{s:11:"category_id";s:1:"4";}'),
(28, 'product', 1, 'accessories/ariel-roll-sleeve-sweatshirt.html', 'catalog/product/view/id/1/category/5', 0, 2, NULL, 1, 'a:1:{s:11:"category_id";s:1:"5";}'),
(31, 'product', 2, 'arcadio-gym-short-32-blue.html', 'catalog/product/view/id/2', 0, 1, NULL, 1, NULL),
(32, 'product', 2, 'women/arcadio-gym-short-32-blue.html', 'catalog/product/view/id/2/category/3', 0, 1, NULL, 1, 'a:1:{s:11:"category_id";s:1:"3";}'),
(33, 'product', 2, 'mens/arcadio-gym-short-32-blue.html', 'catalog/product/view/id/2/category/4', 0, 1, NULL, 1, 'a:1:{s:11:"category_id";s:1:"4";}'),
(34, 'product', 2, 'accessories/arcadio-gym-short-32-blue.html', 'catalog/product/view/id/2/category/5', 0, 1, NULL, 1, 'a:1:{s:11:"category_id";s:1:"5";}'),
(35, 'product', 2, 'arcadio-gym-short-32-blue.html', 'catalog/product/view/id/2', 0, 2, NULL, 1, NULL),
(36, 'product', 2, 'women/arcadio-gym-short-32-blue.html', 'catalog/product/view/id/2/category/3', 0, 2, NULL, 1, 'a:1:{s:11:"category_id";s:1:"3";}'),
(37, 'product', 2, 'mens/arcadio-gym-short-32-blue.html', 'catalog/product/view/id/2/category/4', 0, 2, NULL, 1, 'a:1:{s:11:"category_id";s:1:"4";}'),
(38, 'product', 2, 'accessories/arcadio-gym-short-32-blue.html', 'catalog/product/view/id/2/category/5', 0, 2, NULL, 1, 'a:1:{s:11:"category_id";s:1:"5";}'),
(39, 'product', 3, 'atomic-endurance-running-tee.html', 'catalog/product/view/id/3', 0, 1, NULL, 1, NULL),
(40, 'product', 3, 'women/atomic-endurance-running-tee.html', 'catalog/product/view/id/3/category/3', 0, 1, NULL, 1, 'a:1:{s:11:"category_id";s:1:"3";}'),
(41, 'product', 3, 'mens/atomic-endurance-running-tee.html', 'catalog/product/view/id/3/category/4', 0, 1, NULL, 1, 'a:1:{s:11:"category_id";s:1:"4";}'),
(42, 'product', 3, 'accessories/atomic-endurance-running-tee.html', 'catalog/product/view/id/3/category/5', 0, 1, NULL, 1, 'a:1:{s:11:"category_id";s:1:"5";}'),
(43, 'product', 3, 'atomic-endurance-running-tee.html', 'catalog/product/view/id/3', 0, 2, NULL, 1, NULL),
(44, 'product', 3, 'women/atomic-endurance-running-tee.html', 'catalog/product/view/id/3/category/3', 0, 2, NULL, 1, 'a:1:{s:11:"category_id";s:1:"3";}'),
(45, 'product', 3, 'mens/atomic-endurance-running-tee.html', 'catalog/product/view/id/3/category/4', 0, 2, NULL, 1, 'a:1:{s:11:"category_id";s:1:"4";}'),
(46, 'product', 3, 'accessories/atomic-endurance-running-tee.html', 'catalog/product/view/id/3/category/5', 0, 2, NULL, 1, 'a:1:{s:11:"category_id";s:1:"5";}'),
(47, 'product', 4, 'arcadio-gym-short.html', 'catalog/product/view/id/4', 0, 1, NULL, 1, NULL),
(48, 'product', 4, 'women/arcadio-gym-short.html', 'catalog/product/view/id/4/category/3', 0, 1, NULL, 1, 'a:1:{s:11:"category_id";s:1:"3";}'),
(49, 'product', 4, 'mens/arcadio-gym-short.html', 'catalog/product/view/id/4/category/4', 0, 1, NULL, 1, 'a:1:{s:11:"category_id";s:1:"4";}'),
(50, 'product', 4, 'accessories/arcadio-gym-short.html', 'catalog/product/view/id/4/category/5', 0, 1, NULL, 1, 'a:1:{s:11:"category_id";s:1:"5";}'),
(51, 'product', 4, 'arcadio-gym-short.html', 'catalog/product/view/id/4', 0, 2, NULL, 1, NULL),
(52, 'product', 4, 'women/arcadio-gym-short.html', 'catalog/product/view/id/4/category/3', 0, 2, NULL, 1, 'a:1:{s:11:"category_id";s:1:"3";}'),
(53, 'product', 4, 'mens/arcadio-gym-short.html', 'catalog/product/view/id/4/category/4', 0, 2, NULL, 1, 'a:1:{s:11:"category_id";s:1:"4";}'),
(54, 'product', 4, 'accessories/arcadio-gym-short.html', 'catalog/product/view/id/4/category/5', 0, 2, NULL, 1, 'a:1:{s:11:"category_id";s:1:"5";}'),
(55, 'product', 5, 'product-configuration-magento.html', 'catalog/product/view/id/5', 0, 1, NULL, 1, NULL),
(56, 'product', 5, 'women/product-configuration-magento.html', 'catalog/product/view/id/5/category/3', 0, 1, NULL, 1, 'a:1:{s:11:"category_id";s:1:"3";}'),
(57, 'product', 5, 'mens/product-configuration-magento.html', 'catalog/product/view/id/5/category/4', 0, 1, NULL, 1, 'a:1:{s:11:"category_id";s:1:"4";}'),
(58, 'product', 5, 'accessories/product-configuration-magento.html', 'catalog/product/view/id/5/category/5', 0, 1, NULL, 1, 'a:1:{s:11:"category_id";s:1:"5";}'),
(59, 'product', 5, 'product-configuration-magento.html', 'catalog/product/view/id/5', 0, 2, NULL, 1, NULL),
(60, 'product', 5, 'women/product-configuration-magento.html', 'catalog/product/view/id/5/category/3', 0, 2, NULL, 1, 'a:1:{s:11:"category_id";s:1:"3";}'),
(61, 'product', 5, 'mens/product-configuration-magento.html', 'catalog/product/view/id/5/category/4', 0, 2, NULL, 1, 'a:1:{s:11:"category_id";s:1:"4";}'),
(62, 'product', 5, 'accessories/product-configuration-magento.html', 'catalog/product/view/id/5/category/5', 0, 2, NULL, 1, 'a:1:{s:11:"category_id";s:1:"5";}'),
(67, 'cms-page', 5, 'blog-detail', 'cms/page/view/page_id/5', 0, 1, NULL, 1, NULL),
(68, 'cms-page', 5, 'blog-detail', 'cms/page/view/page_id/5', 0, 2, NULL, 1, NULL),
(69, 'category', 6, 'blog.html', 'catalog/category/view/id/6', 0, 1, NULL, 1, NULL),
(70, 'category', 6, 'blog.html', 'catalog/category/view/id/6', 0, 2, NULL, 1, NULL),
(71, 'category', 7, 'about-us.html', 'catalog/category/view/id/7', 0, 1, NULL, 1, NULL),
(72, 'category', 7, 'about-us.html', 'catalog/category/view/id/7', 0, 2, NULL, 1, NULL),
(73, 'product', 9, 'magento-bundle-product-type.html', 'catalog/product/view/id/9', 0, 1, NULL, 1, NULL),
(74, 'product', 9, 'women/magento-bundle-product-type.html', 'catalog/product/view/id/9/category/3', 0, 1, NULL, 1, 'a:1:{s:11:"category_id";s:1:"3";}'),
(75, 'product', 9, 'mens/magento-bundle-product-type.html', 'catalog/product/view/id/9/category/4', 0, 1, NULL, 1, 'a:1:{s:11:"category_id";s:1:"4";}'),
(76, 'product', 9, 'accessories/magento-bundle-product-type.html', 'catalog/product/view/id/9/category/5', 0, 1, NULL, 1, 'a:1:{s:11:"category_id";s:1:"5";}'),
(77, 'product', 9, 'magento-bundle-product-type.html', 'catalog/product/view/id/9', 0, 2, NULL, 1, NULL),
(78, 'product', 9, 'women/magento-bundle-product-type.html', 'catalog/product/view/id/9/category/3', 0, 2, NULL, 1, 'a:1:{s:11:"category_id";s:1:"3";}'),
(79, 'product', 9, 'mens/magento-bundle-product-type.html', 'catalog/product/view/id/9/category/4', 0, 2, NULL, 1, 'a:1:{s:11:"category_id";s:1:"4";}'),
(80, 'product', 9, 'accessories/magento-bundle-product-type.html', 'catalog/product/view/id/9/category/5', 0, 2, NULL, 1, 'a:1:{s:11:"category_id";s:1:"5";}'),
(81, 'product', 10, 'grouped-products.html', 'catalog/product/view/id/10', 0, 1, NULL, 1, NULL),
(82, 'product', 10, 'grouped-products.html', 'catalog/product/view/id/10', 0, 2, NULL, 1, NULL),
(91, 'product', 12, 'ariel-roll-sleeve-sweatshirt-women.html', 'catalog/product/view/id/12', 0, 1, NULL, 1, NULL),
(92, 'product', 12, 'women/ariel-roll-sleeve-sweatshirt-women.html', 'catalog/product/view/id/12/category/3', 0, 1, NULL, 1, 'a:1:{s:11:"category_id";s:1:"3";}'),
(93, 'product', 12, 'mens/ariel-roll-sleeve-sweatshirt-women.html', 'catalog/product/view/id/12/category/4', 0, 1, NULL, 1, 'a:1:{s:11:"category_id";s:1:"4";}'),
(94, 'product', 12, 'accessories/ariel-roll-sleeve-sweatshirt-women.html', 'catalog/product/view/id/12/category/5', 0, 1, NULL, 1, 'a:1:{s:11:"category_id";s:1:"5";}'),
(95, 'product', 12, 'ariel-roll-sleeve-sweatshirt-women.html', 'catalog/product/view/id/12', 0, 2, NULL, 1, NULL),
(96, 'product', 12, 'women/ariel-roll-sleeve-sweatshirt-women.html', 'catalog/product/view/id/12/category/3', 0, 2, NULL, 1, 'a:1:{s:11:"category_id";s:1:"3";}'),
(97, 'product', 12, 'mens/ariel-roll-sleeve-sweatshirt-women.html', 'catalog/product/view/id/12/category/4', 0, 2, NULL, 1, 'a:1:{s:11:"category_id";s:1:"4";}'),
(98, 'product', 12, 'accessories/ariel-roll-sleeve-sweatshirt-women.html', 'catalog/product/view/id/12/category/5', 0, 2, NULL, 1, 'a:1:{s:11:"category_id";s:1:"5";}');

-- --------------------------------------------------------

--
-- Table structure for table `variable`
--

CREATE TABLE `variable` (
  `variable_id` int(10) UNSIGNED NOT NULL COMMENT 'Variable Id',
  `code` varchar(255) DEFAULT NULL COMMENT 'Variable Code',
  `name` varchar(255) DEFAULT NULL COMMENT 'Variable Name'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Variables';

-- --------------------------------------------------------

--
-- Table structure for table `variable_value`
--

CREATE TABLE `variable_value` (
  `value_id` int(10) UNSIGNED NOT NULL COMMENT 'Variable Value Id',
  `variable_id` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Variable Id',
  `store_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Store Id',
  `plain_value` text COMMENT 'Plain Text Value',
  `html_value` text COMMENT 'Html Value'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Variable Value';

-- --------------------------------------------------------

--
-- Table structure for table `weee_tax`
--

CREATE TABLE `weee_tax` (
  `value_id` int(11) NOT NULL COMMENT 'Value Id',
  `website_id` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Website Id',
  `entity_id` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Entity Id',
  `country` varchar(2) DEFAULT NULL COMMENT 'Country',
  `value` decimal(12,4) NOT NULL DEFAULT '0.0000' COMMENT 'Value',
  `state` int(11) NOT NULL DEFAULT '0' COMMENT 'State',
  `attribute_id` smallint(5) UNSIGNED NOT NULL COMMENT 'Attribute Id'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Weee Tax';

-- --------------------------------------------------------

--
-- Table structure for table `widget`
--

CREATE TABLE `widget` (
  `widget_id` int(10) UNSIGNED NOT NULL COMMENT 'Widget Id',
  `widget_code` varchar(255) DEFAULT NULL COMMENT 'Widget code for template directive',
  `widget_type` varchar(255) DEFAULT NULL COMMENT 'Widget Type',
  `parameters` text COMMENT 'Parameters'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Preconfigured Widgets';

-- --------------------------------------------------------

--
-- Table structure for table `widget_instance`
--

CREATE TABLE `widget_instance` (
  `instance_id` int(10) UNSIGNED NOT NULL COMMENT 'Instance Id',
  `instance_type` varchar(255) DEFAULT NULL COMMENT 'Instance Type',
  `theme_id` int(10) UNSIGNED NOT NULL COMMENT 'Theme id',
  `title` varchar(255) DEFAULT NULL COMMENT 'Widget Title',
  `store_ids` varchar(255) NOT NULL DEFAULT '0' COMMENT 'Store ids',
  `widget_parameters` text COMMENT 'Widget parameters',
  `sort_order` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Sort order'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Instances of Widget for Package Theme';

-- --------------------------------------------------------

--
-- Table structure for table `widget_instance_page`
--

CREATE TABLE `widget_instance_page` (
  `page_id` int(10) UNSIGNED NOT NULL COMMENT 'Page Id',
  `instance_id` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Instance Id',
  `page_group` varchar(25) DEFAULT NULL COMMENT 'Block Group Type',
  `layout_handle` varchar(255) DEFAULT NULL COMMENT 'Layout Handle',
  `block_reference` varchar(255) DEFAULT NULL COMMENT 'Container',
  `page_for` varchar(25) DEFAULT NULL COMMENT 'For instance entities',
  `entities` text COMMENT 'Catalog entities (comma separated)',
  `page_template` varchar(255) DEFAULT NULL COMMENT 'Path to widget template'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Instance of Widget on Page';

-- --------------------------------------------------------

--
-- Table structure for table `widget_instance_page_layout`
--

CREATE TABLE `widget_instance_page_layout` (
  `page_id` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Page Id',
  `layout_update_id` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Layout Update Id'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Layout updates';

-- --------------------------------------------------------

--
-- Table structure for table `wishlist`
--

CREATE TABLE `wishlist` (
  `wishlist_id` int(10) UNSIGNED NOT NULL COMMENT 'Wishlist ID',
  `customer_id` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Customer ID',
  `shared` smallint(5) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Sharing flag (0 or 1)',
  `sharing_code` varchar(32) DEFAULT NULL COMMENT 'Sharing encrypted code',
  `updated_at` timestamp NULL DEFAULT NULL COMMENT 'Last updated date'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Wishlist main Table';

--
-- Dumping data for table `wishlist`
--

INSERT INTO `wishlist` (`wishlist_id`, `customer_id`, `shared`, `sharing_code`, `updated_at`) VALUES
(1, 2, 0, '02e75267a264d5d5bac03be8cdd7f5f6', '2016-04-28 02:43:13');

-- --------------------------------------------------------

--
-- Table structure for table `wishlist_item`
--

CREATE TABLE `wishlist_item` (
  `wishlist_item_id` int(10) UNSIGNED NOT NULL COMMENT 'Wishlist item ID',
  `wishlist_id` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Wishlist ID',
  `product_id` int(10) UNSIGNED NOT NULL DEFAULT '0' COMMENT 'Product ID',
  `store_id` smallint(5) UNSIGNED DEFAULT NULL COMMENT 'Store ID',
  `added_at` timestamp NULL DEFAULT NULL COMMENT 'Add date and time',
  `description` text COMMENT 'Short description of wish list item',
  `qty` decimal(12,4) NOT NULL COMMENT 'Qty'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Wishlist items';

-- --------------------------------------------------------

--
-- Table structure for table `wishlist_item_option`
--

CREATE TABLE `wishlist_item_option` (
  `option_id` int(10) UNSIGNED NOT NULL COMMENT 'Option Id',
  `wishlist_item_id` int(10) UNSIGNED NOT NULL COMMENT 'Wishlist Item Id',
  `product_id` int(10) UNSIGNED NOT NULL COMMENT 'Product Id',
  `code` varchar(255) NOT NULL COMMENT 'Code',
  `value` text COMMENT 'Value'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Wishlist Item Option Table';

--
-- Indexes for dumped tables
--

--
-- Indexes for table `adminnotification_inbox`
--
ALTER TABLE `adminnotification_inbox`
  ADD PRIMARY KEY (`notification_id`),
  ADD KEY `ADMINNOTIFICATION_INBOX_SEVERITY` (`severity`),
  ADD KEY `ADMINNOTIFICATION_INBOX_IS_READ` (`is_read`),
  ADD KEY `ADMINNOTIFICATION_INBOX_IS_REMOVE` (`is_remove`);

--
-- Indexes for table `admin_passwords`
--
ALTER TABLE `admin_passwords`
  ADD PRIMARY KEY (`password_id`),
  ADD KEY `ADMIN_PASSWORDS_USER_ID` (`user_id`);

--
-- Indexes for table `admin_system_messages`
--
ALTER TABLE `admin_system_messages`
  ADD PRIMARY KEY (`identity`);

--
-- Indexes for table `admin_user`
--
ALTER TABLE `admin_user`
  ADD PRIMARY KEY (`user_id`),
  ADD UNIQUE KEY `ADMIN_USER_USERNAME` (`username`);

--
-- Indexes for table `authorization_role`
--
ALTER TABLE `authorization_role`
  ADD PRIMARY KEY (`role_id`),
  ADD KEY `AUTHORIZATION_ROLE_PARENT_ID_SORT_ORDER` (`parent_id`,`sort_order`),
  ADD KEY `AUTHORIZATION_ROLE_TREE_LEVEL` (`tree_level`);

--
-- Indexes for table `authorization_rule`
--
ALTER TABLE `authorization_rule`
  ADD PRIMARY KEY (`rule_id`),
  ADD KEY `AUTHORIZATION_RULE_RESOURCE_ID_ROLE_ID` (`resource_id`,`role_id`),
  ADD KEY `AUTHORIZATION_RULE_ROLE_ID_RESOURCE_ID` (`role_id`,`resource_id`);

--
-- Indexes for table `cache`
--
ALTER TABLE `cache`
  ADD PRIMARY KEY (`id`),
  ADD KEY `CACHE_EXPIRE_TIME` (`expire_time`);

--
-- Indexes for table `cache_tag`
--
ALTER TABLE `cache_tag`
  ADD PRIMARY KEY (`tag`,`cache_id`),
  ADD KEY `CACHE_TAG_CACHE_ID` (`cache_id`);

--
-- Indexes for table `captcha_log`
--
ALTER TABLE `captcha_log`
  ADD PRIMARY KEY (`type`,`value`);

--
-- Indexes for table `cataloginventory_stock`
--
ALTER TABLE `cataloginventory_stock`
  ADD PRIMARY KEY (`stock_id`),
  ADD KEY `CATALOGINVENTORY_STOCK_WEBSITE_ID` (`website_id`);

--
-- Indexes for table `cataloginventory_stock_item`
--
ALTER TABLE `cataloginventory_stock_item`
  ADD PRIMARY KEY (`item_id`),
  ADD UNIQUE KEY `CATALOGINVENTORY_STOCK_ITEM_PRODUCT_ID_WEBSITE_ID` (`product_id`,`website_id`),
  ADD KEY `CATALOGINVENTORY_STOCK_ITEM_WEBSITE_ID` (`website_id`),
  ADD KEY `CATALOGINVENTORY_STOCK_ITEM_STOCK_ID` (`stock_id`);

--
-- Indexes for table `cataloginventory_stock_status`
--
ALTER TABLE `cataloginventory_stock_status`
  ADD PRIMARY KEY (`product_id`,`website_id`,`stock_id`),
  ADD KEY `CATALOGINVENTORY_STOCK_STATUS_STOCK_ID` (`stock_id`),
  ADD KEY `CATALOGINVENTORY_STOCK_STATUS_WEBSITE_ID` (`website_id`);

--
-- Indexes for table `cataloginventory_stock_status_idx`
--
ALTER TABLE `cataloginventory_stock_status_idx`
  ADD PRIMARY KEY (`product_id`,`website_id`,`stock_id`),
  ADD KEY `CATALOGINVENTORY_STOCK_STATUS_IDX_STOCK_ID` (`stock_id`),
  ADD KEY `CATALOGINVENTORY_STOCK_STATUS_IDX_WEBSITE_ID` (`website_id`);

--
-- Indexes for table `cataloginventory_stock_status_tmp`
--
ALTER TABLE `cataloginventory_stock_status_tmp`
  ADD PRIMARY KEY (`product_id`,`website_id`,`stock_id`),
  ADD KEY `CATALOGINVENTORY_STOCK_STATUS_TMP_STOCK_ID` (`stock_id`),
  ADD KEY `CATALOGINVENTORY_STOCK_STATUS_TMP_WEBSITE_ID` (`website_id`);

--
-- Indexes for table `catalogrule`
--
ALTER TABLE `catalogrule`
  ADD PRIMARY KEY (`rule_id`),
  ADD KEY `CATALOGRULE_IS_ACTIVE_SORT_ORDER_TO_DATE_FROM_DATE` (`is_active`,`sort_order`,`to_date`,`from_date`);

--
-- Indexes for table `catalogrule_customer_group`
--
ALTER TABLE `catalogrule_customer_group`
  ADD PRIMARY KEY (`rule_id`,`customer_group_id`),
  ADD KEY `CATALOGRULE_CUSTOMER_GROUP_CUSTOMER_GROUP_ID` (`customer_group_id`);

--
-- Indexes for table `catalogrule_group_website`
--
ALTER TABLE `catalogrule_group_website`
  ADD PRIMARY KEY (`rule_id`,`customer_group_id`,`website_id`),
  ADD KEY `CATALOGRULE_GROUP_WEBSITE_CUSTOMER_GROUP_ID` (`customer_group_id`),
  ADD KEY `CATALOGRULE_GROUP_WEBSITE_WEBSITE_ID` (`website_id`);

--
-- Indexes for table `catalogrule_product`
--
ALTER TABLE `catalogrule_product`
  ADD PRIMARY KEY (`rule_product_id`),
  ADD UNIQUE KEY `IDX_EAA51B56FF092A0DCB795D1CEF812B7B` (`rule_id`,`from_time`,`to_time`,`website_id`,`customer_group_id`,`product_id`,`sort_order`),
  ADD KEY `CATALOGRULE_PRODUCT_CUSTOMER_GROUP_ID` (`customer_group_id`),
  ADD KEY `CATALOGRULE_PRODUCT_WEBSITE_ID` (`website_id`),
  ADD KEY `CATALOGRULE_PRODUCT_FROM_TIME` (`from_time`),
  ADD KEY `CATALOGRULE_PRODUCT_TO_TIME` (`to_time`),
  ADD KEY `CATALOGRULE_PRODUCT_PRODUCT_ID` (`product_id`);

--
-- Indexes for table `catalogrule_product_price`
--
ALTER TABLE `catalogrule_product_price`
  ADD PRIMARY KEY (`rule_product_price_id`),
  ADD UNIQUE KEY `CATRULE_PRD_PRICE_RULE_DATE_WS_ID_CSTR_GROUP_ID_PRD_ID` (`rule_date`,`website_id`,`customer_group_id`,`product_id`),
  ADD KEY `CATALOGRULE_PRODUCT_PRICE_CUSTOMER_GROUP_ID` (`customer_group_id`),
  ADD KEY `CATALOGRULE_PRODUCT_PRICE_WEBSITE_ID` (`website_id`),
  ADD KEY `CATALOGRULE_PRODUCT_PRICE_PRODUCT_ID` (`product_id`);

--
-- Indexes for table `catalogrule_website`
--
ALTER TABLE `catalogrule_website`
  ADD PRIMARY KEY (`rule_id`,`website_id`),
  ADD KEY `CATALOGRULE_WEBSITE_WEBSITE_ID` (`website_id`);

--
-- Indexes for table `catalogsearch_fulltext_scope1`
--
ALTER TABLE `catalogsearch_fulltext_scope1`
  ADD PRIMARY KEY (`entity_id`,`attribute_id`);
ALTER TABLE `catalogsearch_fulltext_scope1` ADD FULLTEXT KEY `FTI_FULLTEXT_DATA_INDEX` (`data_index`);

--
-- Indexes for table `catalogsearch_fulltext_scope2`
--
ALTER TABLE `catalogsearch_fulltext_scope2`
  ADD PRIMARY KEY (`entity_id`,`attribute_id`);
ALTER TABLE `catalogsearch_fulltext_scope2` ADD FULLTEXT KEY `FTI_FULLTEXT_DATA_INDEX` (`data_index`);

--
-- Indexes for table `catalog_category_entity`
--
ALTER TABLE `catalog_category_entity`
  ADD PRIMARY KEY (`entity_id`),
  ADD KEY `CATALOG_CATEGORY_ENTITY_LEVEL` (`level`);

--
-- Indexes for table `catalog_category_entity_datetime`
--
ALTER TABLE `catalog_category_entity_datetime`
  ADD PRIMARY KEY (`value_id`),
  ADD UNIQUE KEY `CATALOG_CATEGORY_ENTITY_DATETIME_ENTITY_ID_ATTRIBUTE_ID_STORE_ID` (`entity_id`,`attribute_id`,`store_id`),
  ADD KEY `CATALOG_CATEGORY_ENTITY_DATETIME_ENTITY_ID` (`entity_id`),
  ADD KEY `CATALOG_CATEGORY_ENTITY_DATETIME_ATTRIBUTE_ID` (`attribute_id`),
  ADD KEY `CATALOG_CATEGORY_ENTITY_DATETIME_STORE_ID` (`store_id`);

--
-- Indexes for table `catalog_category_entity_decimal`
--
ALTER TABLE `catalog_category_entity_decimal`
  ADD PRIMARY KEY (`value_id`),
  ADD UNIQUE KEY `CATALOG_CATEGORY_ENTITY_DECIMAL_ENTITY_ID_ATTRIBUTE_ID_STORE_ID` (`entity_id`,`attribute_id`,`store_id`),
  ADD KEY `CATALOG_CATEGORY_ENTITY_DECIMAL_ENTITY_ID` (`entity_id`),
  ADD KEY `CATALOG_CATEGORY_ENTITY_DECIMAL_ATTRIBUTE_ID` (`attribute_id`),
  ADD KEY `CATALOG_CATEGORY_ENTITY_DECIMAL_STORE_ID` (`store_id`);

--
-- Indexes for table `catalog_category_entity_int`
--
ALTER TABLE `catalog_category_entity_int`
  ADD PRIMARY KEY (`value_id`),
  ADD UNIQUE KEY `CATALOG_CATEGORY_ENTITY_INT_ENTITY_ID_ATTRIBUTE_ID_STORE_ID` (`entity_id`,`attribute_id`,`store_id`),
  ADD KEY `CATALOG_CATEGORY_ENTITY_INT_ENTITY_ID` (`entity_id`),
  ADD KEY `CATALOG_CATEGORY_ENTITY_INT_ATTRIBUTE_ID` (`attribute_id`),
  ADD KEY `CATALOG_CATEGORY_ENTITY_INT_STORE_ID` (`store_id`);

--
-- Indexes for table `catalog_category_entity_text`
--
ALTER TABLE `catalog_category_entity_text`
  ADD PRIMARY KEY (`value_id`),
  ADD UNIQUE KEY `CATALOG_CATEGORY_ENTITY_TEXT_ENTITY_ID_ATTRIBUTE_ID_STORE_ID` (`entity_id`,`attribute_id`,`store_id`),
  ADD KEY `CATALOG_CATEGORY_ENTITY_TEXT_ENTITY_ID` (`entity_id`),
  ADD KEY `CATALOG_CATEGORY_ENTITY_TEXT_ATTRIBUTE_ID` (`attribute_id`),
  ADD KEY `CATALOG_CATEGORY_ENTITY_TEXT_STORE_ID` (`store_id`);

--
-- Indexes for table `catalog_category_entity_varchar`
--
ALTER TABLE `catalog_category_entity_varchar`
  ADD PRIMARY KEY (`value_id`),
  ADD UNIQUE KEY `CATALOG_CATEGORY_ENTITY_VARCHAR_ENTITY_ID_ATTRIBUTE_ID_STORE_ID` (`entity_id`,`attribute_id`,`store_id`),
  ADD KEY `CATALOG_CATEGORY_ENTITY_VARCHAR_ENTITY_ID` (`entity_id`),
  ADD KEY `CATALOG_CATEGORY_ENTITY_VARCHAR_ATTRIBUTE_ID` (`attribute_id`),
  ADD KEY `CATALOG_CATEGORY_ENTITY_VARCHAR_STORE_ID` (`store_id`);

--
-- Indexes for table `catalog_category_product`
--
ALTER TABLE `catalog_category_product`
  ADD PRIMARY KEY (`category_id`,`product_id`),
  ADD KEY `CATALOG_CATEGORY_PRODUCT_PRODUCT_ID` (`product_id`);

--
-- Indexes for table `catalog_category_product_index`
--
ALTER TABLE `catalog_category_product_index`
  ADD PRIMARY KEY (`category_id`,`product_id`,`store_id`),
  ADD KEY `CAT_CTGR_PRD_IDX_PRD_ID_STORE_ID_CTGR_ID_VISIBILITY` (`product_id`,`store_id`,`category_id`,`visibility`),
  ADD KEY `CAT_CTGR_PRD_IDX_STORE_ID_CTGR_ID_VISIBILITY_IS_PARENT_POSITION` (`store_id`,`category_id`,`visibility`,`is_parent`,`position`);

--
-- Indexes for table `catalog_category_product_index_tmp`
--
ALTER TABLE `catalog_category_product_index_tmp`
  ADD KEY `CAT_CTGR_PRD_IDX_TMP_PRD_ID_CTGR_ID_STORE_ID` (`product_id`,`category_id`,`store_id`);

--
-- Indexes for table `catalog_compare_item`
--
ALTER TABLE `catalog_compare_item`
  ADD PRIMARY KEY (`catalog_compare_item_id`),
  ADD KEY `CATALOG_COMPARE_ITEM_PRODUCT_ID` (`product_id`),
  ADD KEY `CATALOG_COMPARE_ITEM_VISITOR_ID_PRODUCT_ID` (`visitor_id`,`product_id`),
  ADD KEY `CATALOG_COMPARE_ITEM_CUSTOMER_ID_PRODUCT_ID` (`customer_id`,`product_id`),
  ADD KEY `CATALOG_COMPARE_ITEM_STORE_ID` (`store_id`);

--
-- Indexes for table `catalog_eav_attribute`
--
ALTER TABLE `catalog_eav_attribute`
  ADD PRIMARY KEY (`attribute_id`),
  ADD KEY `CATALOG_EAV_ATTRIBUTE_USED_FOR_SORT_BY` (`used_for_sort_by`),
  ADD KEY `CATALOG_EAV_ATTRIBUTE_USED_IN_PRODUCT_LISTING` (`used_in_product_listing`);

--
-- Indexes for table `catalog_product_bundle_option`
--
ALTER TABLE `catalog_product_bundle_option`
  ADD PRIMARY KEY (`option_id`),
  ADD KEY `CATALOG_PRODUCT_BUNDLE_OPTION_PARENT_ID` (`parent_id`);

--
-- Indexes for table `catalog_product_bundle_option_value`
--
ALTER TABLE `catalog_product_bundle_option_value`
  ADD PRIMARY KEY (`value_id`),
  ADD UNIQUE KEY `CATALOG_PRODUCT_BUNDLE_OPTION_VALUE_OPTION_ID_STORE_ID` (`option_id`,`store_id`);

--
-- Indexes for table `catalog_product_bundle_price_index`
--
ALTER TABLE `catalog_product_bundle_price_index`
  ADD PRIMARY KEY (`entity_id`,`website_id`,`customer_group_id`),
  ADD KEY `CATALOG_PRODUCT_BUNDLE_PRICE_INDEX_WEBSITE_ID` (`website_id`),
  ADD KEY `CATALOG_PRODUCT_BUNDLE_PRICE_INDEX_CUSTOMER_GROUP_ID` (`customer_group_id`);

--
-- Indexes for table `catalog_product_bundle_selection`
--
ALTER TABLE `catalog_product_bundle_selection`
  ADD PRIMARY KEY (`selection_id`),
  ADD KEY `CATALOG_PRODUCT_BUNDLE_SELECTION_OPTION_ID` (`option_id`),
  ADD KEY `CATALOG_PRODUCT_BUNDLE_SELECTION_PRODUCT_ID` (`product_id`);

--
-- Indexes for table `catalog_product_bundle_selection_price`
--
ALTER TABLE `catalog_product_bundle_selection_price`
  ADD PRIMARY KEY (`selection_id`,`website_id`),
  ADD KEY `CATALOG_PRODUCT_BUNDLE_SELECTION_PRICE_WEBSITE_ID` (`website_id`);

--
-- Indexes for table `catalog_product_bundle_stock_index`
--
ALTER TABLE `catalog_product_bundle_stock_index`
  ADD PRIMARY KEY (`entity_id`,`website_id`,`stock_id`,`option_id`);

--
-- Indexes for table `catalog_product_entity`
--
ALTER TABLE `catalog_product_entity`
  ADD PRIMARY KEY (`entity_id`),
  ADD KEY `CATALOG_PRODUCT_ENTITY_ATTRIBUTE_SET_ID` (`attribute_set_id`),
  ADD KEY `CATALOG_PRODUCT_ENTITY_SKU` (`sku`);

--
-- Indexes for table `catalog_product_entity_datetime`
--
ALTER TABLE `catalog_product_entity_datetime`
  ADD PRIMARY KEY (`value_id`),
  ADD UNIQUE KEY `CATALOG_PRODUCT_ENTITY_DATETIME_ENTITY_ID_ATTRIBUTE_ID_STORE_ID` (`entity_id`,`attribute_id`,`store_id`),
  ADD KEY `CATALOG_PRODUCT_ENTITY_DATETIME_ATTRIBUTE_ID` (`attribute_id`),
  ADD KEY `CATALOG_PRODUCT_ENTITY_DATETIME_STORE_ID` (`store_id`);

--
-- Indexes for table `catalog_product_entity_decimal`
--
ALTER TABLE `catalog_product_entity_decimal`
  ADD PRIMARY KEY (`value_id`),
  ADD UNIQUE KEY `CATALOG_PRODUCT_ENTITY_DECIMAL_ENTITY_ID_ATTRIBUTE_ID_STORE_ID` (`entity_id`,`attribute_id`,`store_id`),
  ADD KEY `CATALOG_PRODUCT_ENTITY_DECIMAL_STORE_ID` (`store_id`),
  ADD KEY `CATALOG_PRODUCT_ENTITY_DECIMAL_ATTRIBUTE_ID` (`attribute_id`);

--
-- Indexes for table `catalog_product_entity_gallery`
--
ALTER TABLE `catalog_product_entity_gallery`
  ADD PRIMARY KEY (`value_id`),
  ADD UNIQUE KEY `CATALOG_PRODUCT_ENTITY_GALLERY_ENTITY_ID_ATTRIBUTE_ID_STORE_ID` (`entity_id`,`attribute_id`,`store_id`),
  ADD KEY `CATALOG_PRODUCT_ENTITY_GALLERY_ENTITY_ID` (`entity_id`),
  ADD KEY `CATALOG_PRODUCT_ENTITY_GALLERY_ATTRIBUTE_ID` (`attribute_id`),
  ADD KEY `CATALOG_PRODUCT_ENTITY_GALLERY_STORE_ID` (`store_id`);

--
-- Indexes for table `catalog_product_entity_int`
--
ALTER TABLE `catalog_product_entity_int`
  ADD PRIMARY KEY (`value_id`),
  ADD UNIQUE KEY `CATALOG_PRODUCT_ENTITY_INT_ENTITY_ID_ATTRIBUTE_ID_STORE_ID` (`entity_id`,`attribute_id`,`store_id`),
  ADD KEY `CATALOG_PRODUCT_ENTITY_INT_ATTRIBUTE_ID` (`attribute_id`),
  ADD KEY `CATALOG_PRODUCT_ENTITY_INT_STORE_ID` (`store_id`);

--
-- Indexes for table `catalog_product_entity_media_gallery`
--
ALTER TABLE `catalog_product_entity_media_gallery`
  ADD PRIMARY KEY (`value_id`),
  ADD KEY `CATALOG_PRODUCT_ENTITY_MEDIA_GALLERY_ATTRIBUTE_ID` (`attribute_id`);

--
-- Indexes for table `catalog_product_entity_media_gallery_value`
--
ALTER TABLE `catalog_product_entity_media_gallery_value`
  ADD PRIMARY KEY (`record_id`),
  ADD KEY `CATALOG_PRODUCT_ENTITY_MEDIA_GALLERY_VALUE_STORE_ID` (`store_id`),
  ADD KEY `CATALOG_PRODUCT_ENTITY_MEDIA_GALLERY_VALUE_ENTITY_ID` (`entity_id`),
  ADD KEY `CATALOG_PRODUCT_ENTITY_MEDIA_GALLERY_VALUE_VALUE_ID` (`value_id`);

--
-- Indexes for table `catalog_product_entity_media_gallery_value_to_entity`
--
ALTER TABLE `catalog_product_entity_media_gallery_value_to_entity`
  ADD UNIQUE KEY `CAT_PRD_ENTT_MDA_GLR_VAL_TO_ENTT_VAL_ID_ENTT_ID` (`value_id`,`entity_id`),
  ADD KEY `CAT_PRD_ENTT_MDA_GLR_VAL_TO_ENTT_ENTT_ID_CAT_PRD_ENTT_ENTT_ID` (`entity_id`);

--
-- Indexes for table `catalog_product_entity_media_gallery_value_video`
--
ALTER TABLE `catalog_product_entity_media_gallery_value_video`
  ADD UNIQUE KEY `CAT_PRD_ENTT_MDA_GLR_VAL_VIDEO_VAL_ID_STORE_ID` (`value_id`,`store_id`),
  ADD KEY `CAT_PRD_ENTT_MDA_GLR_VAL_VIDEO_STORE_ID_STORE_STORE_ID` (`store_id`);

--
-- Indexes for table `catalog_product_entity_text`
--
ALTER TABLE `catalog_product_entity_text`
  ADD PRIMARY KEY (`value_id`),
  ADD UNIQUE KEY `CATALOG_PRODUCT_ENTITY_TEXT_ENTITY_ID_ATTRIBUTE_ID_STORE_ID` (`entity_id`,`attribute_id`,`store_id`),
  ADD KEY `CATALOG_PRODUCT_ENTITY_TEXT_ATTRIBUTE_ID` (`attribute_id`),
  ADD KEY `CATALOG_PRODUCT_ENTITY_TEXT_STORE_ID` (`store_id`);

--
-- Indexes for table `catalog_product_entity_tier_price`
--
ALTER TABLE `catalog_product_entity_tier_price`
  ADD PRIMARY KEY (`value_id`),
  ADD UNIQUE KEY `UNQ_E8AB433B9ACB00343ABB312AD2FAB087` (`entity_id`,`all_groups`,`customer_group_id`,`qty`,`website_id`),
  ADD KEY `CATALOG_PRODUCT_ENTITY_TIER_PRICE_CUSTOMER_GROUP_ID` (`customer_group_id`),
  ADD KEY `CATALOG_PRODUCT_ENTITY_TIER_PRICE_WEBSITE_ID` (`website_id`);

--
-- Indexes for table `catalog_product_entity_varchar`
--
ALTER TABLE `catalog_product_entity_varchar`
  ADD PRIMARY KEY (`value_id`),
  ADD UNIQUE KEY `CATALOG_PRODUCT_ENTITY_VARCHAR_ENTITY_ID_ATTRIBUTE_ID_STORE_ID` (`entity_id`,`attribute_id`,`store_id`),
  ADD KEY `CATALOG_PRODUCT_ENTITY_VARCHAR_ATTRIBUTE_ID` (`attribute_id`),
  ADD KEY `CATALOG_PRODUCT_ENTITY_VARCHAR_STORE_ID` (`store_id`);

--
-- Indexes for table `catalog_product_index_eav`
--
ALTER TABLE `catalog_product_index_eav`
  ADD PRIMARY KEY (`entity_id`,`attribute_id`,`store_id`,`value`),
  ADD KEY `CATALOG_PRODUCT_INDEX_EAV_ATTRIBUTE_ID` (`attribute_id`),
  ADD KEY `CATALOG_PRODUCT_INDEX_EAV_STORE_ID` (`store_id`),
  ADD KEY `CATALOG_PRODUCT_INDEX_EAV_VALUE` (`value`);

--
-- Indexes for table `catalog_product_index_eav_decimal`
--
ALTER TABLE `catalog_product_index_eav_decimal`
  ADD PRIMARY KEY (`entity_id`,`attribute_id`,`store_id`),
  ADD KEY `CATALOG_PRODUCT_INDEX_EAV_DECIMAL_ATTRIBUTE_ID` (`attribute_id`),
  ADD KEY `CATALOG_PRODUCT_INDEX_EAV_DECIMAL_STORE_ID` (`store_id`),
  ADD KEY `CATALOG_PRODUCT_INDEX_EAV_DECIMAL_VALUE` (`value`);

--
-- Indexes for table `catalog_product_index_eav_decimal_idx`
--
ALTER TABLE `catalog_product_index_eav_decimal_idx`
  ADD PRIMARY KEY (`entity_id`,`attribute_id`,`store_id`,`value`),
  ADD KEY `CATALOG_PRODUCT_INDEX_EAV_DECIMAL_IDX_ATTRIBUTE_ID` (`attribute_id`),
  ADD KEY `CATALOG_PRODUCT_INDEX_EAV_DECIMAL_IDX_STORE_ID` (`store_id`),
  ADD KEY `CATALOG_PRODUCT_INDEX_EAV_DECIMAL_IDX_VALUE` (`value`);

--
-- Indexes for table `catalog_product_index_eav_decimal_tmp`
--
ALTER TABLE `catalog_product_index_eav_decimal_tmp`
  ADD PRIMARY KEY (`entity_id`,`attribute_id`,`store_id`),
  ADD KEY `CATALOG_PRODUCT_INDEX_EAV_DECIMAL_TMP_ATTRIBUTE_ID` (`attribute_id`),
  ADD KEY `CATALOG_PRODUCT_INDEX_EAV_DECIMAL_TMP_STORE_ID` (`store_id`),
  ADD KEY `CATALOG_PRODUCT_INDEX_EAV_DECIMAL_TMP_VALUE` (`value`);

--
-- Indexes for table `catalog_product_index_eav_idx`
--
ALTER TABLE `catalog_product_index_eav_idx`
  ADD PRIMARY KEY (`entity_id`,`attribute_id`,`store_id`,`value`),
  ADD KEY `CATALOG_PRODUCT_INDEX_EAV_IDX_ATTRIBUTE_ID` (`attribute_id`),
  ADD KEY `CATALOG_PRODUCT_INDEX_EAV_IDX_STORE_ID` (`store_id`),
  ADD KEY `CATALOG_PRODUCT_INDEX_EAV_IDX_VALUE` (`value`);

--
-- Indexes for table `catalog_product_index_eav_tmp`
--
ALTER TABLE `catalog_product_index_eav_tmp`
  ADD PRIMARY KEY (`entity_id`,`attribute_id`,`store_id`,`value`),
  ADD KEY `CATALOG_PRODUCT_INDEX_EAV_TMP_ATTRIBUTE_ID` (`attribute_id`),
  ADD KEY `CATALOG_PRODUCT_INDEX_EAV_TMP_STORE_ID` (`store_id`),
  ADD KEY `CATALOG_PRODUCT_INDEX_EAV_TMP_VALUE` (`value`);

--
-- Indexes for table `catalog_product_index_price`
--
ALTER TABLE `catalog_product_index_price`
  ADD PRIMARY KEY (`entity_id`,`customer_group_id`,`website_id`),
  ADD KEY `CATALOG_PRODUCT_INDEX_PRICE_CUSTOMER_GROUP_ID` (`customer_group_id`),
  ADD KEY `CATALOG_PRODUCT_INDEX_PRICE_MIN_PRICE` (`min_price`),
  ADD KEY `CAT_PRD_IDX_PRICE_WS_ID_CSTR_GROUP_ID_MIN_PRICE` (`website_id`,`customer_group_id`,`min_price`);

--
-- Indexes for table `catalog_product_index_price_bundle_idx`
--
ALTER TABLE `catalog_product_index_price_bundle_idx`
  ADD PRIMARY KEY (`entity_id`,`customer_group_id`,`website_id`);

--
-- Indexes for table `catalog_product_index_price_bundle_opt_idx`
--
ALTER TABLE `catalog_product_index_price_bundle_opt_idx`
  ADD PRIMARY KEY (`entity_id`,`customer_group_id`,`website_id`,`option_id`);

--
-- Indexes for table `catalog_product_index_price_bundle_opt_tmp`
--
ALTER TABLE `catalog_product_index_price_bundle_opt_tmp`
  ADD PRIMARY KEY (`entity_id`,`customer_group_id`,`website_id`,`option_id`);

--
-- Indexes for table `catalog_product_index_price_bundle_sel_idx`
--
ALTER TABLE `catalog_product_index_price_bundle_sel_idx`
  ADD PRIMARY KEY (`entity_id`,`customer_group_id`,`website_id`,`option_id`,`selection_id`);

--
-- Indexes for table `catalog_product_index_price_bundle_sel_tmp`
--
ALTER TABLE `catalog_product_index_price_bundle_sel_tmp`
  ADD PRIMARY KEY (`entity_id`,`customer_group_id`,`website_id`,`option_id`,`selection_id`);

--
-- Indexes for table `catalog_product_index_price_bundle_tmp`
--
ALTER TABLE `catalog_product_index_price_bundle_tmp`
  ADD PRIMARY KEY (`entity_id`,`customer_group_id`,`website_id`);

--
-- Indexes for table `catalog_product_index_price_cfg_opt_agr_idx`
--
ALTER TABLE `catalog_product_index_price_cfg_opt_agr_idx`
  ADD PRIMARY KEY (`parent_id`,`child_id`,`customer_group_id`,`website_id`);

--
-- Indexes for table `catalog_product_index_price_cfg_opt_agr_tmp`
--
ALTER TABLE `catalog_product_index_price_cfg_opt_agr_tmp`
  ADD PRIMARY KEY (`parent_id`,`child_id`,`customer_group_id`,`website_id`);

--
-- Indexes for table `catalog_product_index_price_cfg_opt_idx`
--
ALTER TABLE `catalog_product_index_price_cfg_opt_idx`
  ADD PRIMARY KEY (`entity_id`,`customer_group_id`,`website_id`);

--
-- Indexes for table `catalog_product_index_price_cfg_opt_tmp`
--
ALTER TABLE `catalog_product_index_price_cfg_opt_tmp`
  ADD PRIMARY KEY (`entity_id`,`customer_group_id`,`website_id`);

--
-- Indexes for table `catalog_product_index_price_downlod_idx`
--
ALTER TABLE `catalog_product_index_price_downlod_idx`
  ADD PRIMARY KEY (`entity_id`,`customer_group_id`,`website_id`);

--
-- Indexes for table `catalog_product_index_price_downlod_tmp`
--
ALTER TABLE `catalog_product_index_price_downlod_tmp`
  ADD PRIMARY KEY (`entity_id`,`customer_group_id`,`website_id`);

--
-- Indexes for table `catalog_product_index_price_final_idx`
--
ALTER TABLE `catalog_product_index_price_final_idx`
  ADD PRIMARY KEY (`entity_id`,`customer_group_id`,`website_id`);

--
-- Indexes for table `catalog_product_index_price_final_tmp`
--
ALTER TABLE `catalog_product_index_price_final_tmp`
  ADD PRIMARY KEY (`entity_id`,`customer_group_id`,`website_id`);

--
-- Indexes for table `catalog_product_index_price_idx`
--
ALTER TABLE `catalog_product_index_price_idx`
  ADD PRIMARY KEY (`entity_id`,`customer_group_id`,`website_id`),
  ADD KEY `CATALOG_PRODUCT_INDEX_PRICE_IDX_CUSTOMER_GROUP_ID` (`customer_group_id`),
  ADD KEY `CATALOG_PRODUCT_INDEX_PRICE_IDX_WEBSITE_ID` (`website_id`),
  ADD KEY `CATALOG_PRODUCT_INDEX_PRICE_IDX_MIN_PRICE` (`min_price`);

--
-- Indexes for table `catalog_product_index_price_opt_agr_idx`
--
ALTER TABLE `catalog_product_index_price_opt_agr_idx`
  ADD PRIMARY KEY (`entity_id`,`customer_group_id`,`website_id`,`option_id`);

--
-- Indexes for table `catalog_product_index_price_opt_agr_tmp`
--
ALTER TABLE `catalog_product_index_price_opt_agr_tmp`
  ADD PRIMARY KEY (`entity_id`,`customer_group_id`,`website_id`,`option_id`);

--
-- Indexes for table `catalog_product_index_price_opt_idx`
--
ALTER TABLE `catalog_product_index_price_opt_idx`
  ADD PRIMARY KEY (`entity_id`,`customer_group_id`,`website_id`);

--
-- Indexes for table `catalog_product_index_price_opt_tmp`
--
ALTER TABLE `catalog_product_index_price_opt_tmp`
  ADD PRIMARY KEY (`entity_id`,`customer_group_id`,`website_id`);

--
-- Indexes for table `catalog_product_index_price_tmp`
--
ALTER TABLE `catalog_product_index_price_tmp`
  ADD PRIMARY KEY (`entity_id`,`customer_group_id`,`website_id`),
  ADD KEY `CATALOG_PRODUCT_INDEX_PRICE_TMP_CUSTOMER_GROUP_ID` (`customer_group_id`),
  ADD KEY `CATALOG_PRODUCT_INDEX_PRICE_TMP_WEBSITE_ID` (`website_id`),
  ADD KEY `CATALOG_PRODUCT_INDEX_PRICE_TMP_MIN_PRICE` (`min_price`);

--
-- Indexes for table `catalog_product_index_tier_price`
--
ALTER TABLE `catalog_product_index_tier_price`
  ADD PRIMARY KEY (`entity_id`,`customer_group_id`,`website_id`),
  ADD KEY `CATALOG_PRODUCT_INDEX_TIER_PRICE_CUSTOMER_GROUP_ID` (`customer_group_id`),
  ADD KEY `CATALOG_PRODUCT_INDEX_TIER_PRICE_WEBSITE_ID` (`website_id`);

--
-- Indexes for table `catalog_product_index_website`
--
ALTER TABLE `catalog_product_index_website`
  ADD PRIMARY KEY (`website_id`),
  ADD KEY `CATALOG_PRODUCT_INDEX_WEBSITE_WEBSITE_DATE` (`website_date`);

--
-- Indexes for table `catalog_product_link`
--
ALTER TABLE `catalog_product_link`
  ADD PRIMARY KEY (`link_id`),
  ADD UNIQUE KEY `CATALOG_PRODUCT_LINK_LINK_TYPE_ID_PRODUCT_ID_LINKED_PRODUCT_ID` (`link_type_id`,`product_id`,`linked_product_id`),
  ADD KEY `CATALOG_PRODUCT_LINK_PRODUCT_ID` (`product_id`),
  ADD KEY `CATALOG_PRODUCT_LINK_LINKED_PRODUCT_ID` (`linked_product_id`);

--
-- Indexes for table `catalog_product_link_attribute`
--
ALTER TABLE `catalog_product_link_attribute`
  ADD PRIMARY KEY (`product_link_attribute_id`),
  ADD KEY `CATALOG_PRODUCT_LINK_ATTRIBUTE_LINK_TYPE_ID` (`link_type_id`);

--
-- Indexes for table `catalog_product_link_attribute_decimal`
--
ALTER TABLE `catalog_product_link_attribute_decimal`
  ADD PRIMARY KEY (`value_id`),
  ADD UNIQUE KEY `CAT_PRD_LNK_ATTR_DEC_PRD_LNK_ATTR_ID_LNK_ID` (`product_link_attribute_id`,`link_id`),
  ADD KEY `CATALOG_PRODUCT_LINK_ATTRIBUTE_DECIMAL_LINK_ID` (`link_id`);

--
-- Indexes for table `catalog_product_link_attribute_int`
--
ALTER TABLE `catalog_product_link_attribute_int`
  ADD PRIMARY KEY (`value_id`),
  ADD UNIQUE KEY `CAT_PRD_LNK_ATTR_INT_PRD_LNK_ATTR_ID_LNK_ID` (`product_link_attribute_id`,`link_id`),
  ADD KEY `CATALOG_PRODUCT_LINK_ATTRIBUTE_INT_LINK_ID` (`link_id`);

--
-- Indexes for table `catalog_product_link_attribute_varchar`
--
ALTER TABLE `catalog_product_link_attribute_varchar`
  ADD PRIMARY KEY (`value_id`),
  ADD UNIQUE KEY `CAT_PRD_LNK_ATTR_VCHR_PRD_LNK_ATTR_ID_LNK_ID` (`product_link_attribute_id`,`link_id`),
  ADD KEY `CATALOG_PRODUCT_LINK_ATTRIBUTE_VARCHAR_LINK_ID` (`link_id`);

--
-- Indexes for table `catalog_product_link_type`
--
ALTER TABLE `catalog_product_link_type`
  ADD PRIMARY KEY (`link_type_id`);

--
-- Indexes for table `catalog_product_option`
--
ALTER TABLE `catalog_product_option`
  ADD PRIMARY KEY (`option_id`),
  ADD KEY `CATALOG_PRODUCT_OPTION_PRODUCT_ID` (`product_id`);

--
-- Indexes for table `catalog_product_option_price`
--
ALTER TABLE `catalog_product_option_price`
  ADD PRIMARY KEY (`option_price_id`),
  ADD UNIQUE KEY `CATALOG_PRODUCT_OPTION_PRICE_OPTION_ID_STORE_ID` (`option_id`,`store_id`),
  ADD KEY `CATALOG_PRODUCT_OPTION_PRICE_STORE_ID` (`store_id`);

--
-- Indexes for table `catalog_product_option_title`
--
ALTER TABLE `catalog_product_option_title`
  ADD PRIMARY KEY (`option_title_id`),
  ADD UNIQUE KEY `CATALOG_PRODUCT_OPTION_TITLE_OPTION_ID_STORE_ID` (`option_id`,`store_id`),
  ADD KEY `CATALOG_PRODUCT_OPTION_TITLE_STORE_ID` (`store_id`);

--
-- Indexes for table `catalog_product_option_type_price`
--
ALTER TABLE `catalog_product_option_type_price`
  ADD PRIMARY KEY (`option_type_price_id`),
  ADD UNIQUE KEY `CATALOG_PRODUCT_OPTION_TYPE_PRICE_OPTION_TYPE_ID_STORE_ID` (`option_type_id`,`store_id`),
  ADD KEY `CATALOG_PRODUCT_OPTION_TYPE_PRICE_STORE_ID` (`store_id`);

--
-- Indexes for table `catalog_product_option_type_title`
--
ALTER TABLE `catalog_product_option_type_title`
  ADD PRIMARY KEY (`option_type_title_id`),
  ADD UNIQUE KEY `CATALOG_PRODUCT_OPTION_TYPE_TITLE_OPTION_TYPE_ID_STORE_ID` (`option_type_id`,`store_id`),
  ADD KEY `CATALOG_PRODUCT_OPTION_TYPE_TITLE_STORE_ID` (`store_id`);

--
-- Indexes for table `catalog_product_option_type_value`
--
ALTER TABLE `catalog_product_option_type_value`
  ADD PRIMARY KEY (`option_type_id`),
  ADD KEY `CATALOG_PRODUCT_OPTION_TYPE_VALUE_OPTION_ID` (`option_id`);

--
-- Indexes for table `catalog_product_relation`
--
ALTER TABLE `catalog_product_relation`
  ADD PRIMARY KEY (`parent_id`,`child_id`),
  ADD KEY `CATALOG_PRODUCT_RELATION_CHILD_ID` (`child_id`);

--
-- Indexes for table `catalog_product_super_attribute`
--
ALTER TABLE `catalog_product_super_attribute`
  ADD PRIMARY KEY (`product_super_attribute_id`),
  ADD UNIQUE KEY `CATALOG_PRODUCT_SUPER_ATTRIBUTE_PRODUCT_ID_ATTRIBUTE_ID` (`product_id`,`attribute_id`);

--
-- Indexes for table `catalog_product_super_attribute_label`
--
ALTER TABLE `catalog_product_super_attribute_label`
  ADD PRIMARY KEY (`value_id`),
  ADD UNIQUE KEY `CAT_PRD_SPR_ATTR_LBL_PRD_SPR_ATTR_ID_STORE_ID` (`product_super_attribute_id`,`store_id`),
  ADD KEY `CATALOG_PRODUCT_SUPER_ATTRIBUTE_LABEL_STORE_ID` (`store_id`);

--
-- Indexes for table `catalog_product_super_link`
--
ALTER TABLE `catalog_product_super_link`
  ADD PRIMARY KEY (`link_id`),
  ADD UNIQUE KEY `CATALOG_PRODUCT_SUPER_LINK_PRODUCT_ID_PARENT_ID` (`product_id`,`parent_id`),
  ADD KEY `CATALOG_PRODUCT_SUPER_LINK_PARENT_ID` (`parent_id`);

--
-- Indexes for table `catalog_product_website`
--
ALTER TABLE `catalog_product_website`
  ADD PRIMARY KEY (`product_id`,`website_id`),
  ADD KEY `CATALOG_PRODUCT_WEBSITE_WEBSITE_ID` (`website_id`);

--
-- Indexes for table `catalog_url_rewrite_product_category`
--
ALTER TABLE `catalog_url_rewrite_product_category`
  ADD KEY `CATALOG_URL_REWRITE_PRODUCT_CATEGORY_CATEGORY_ID_PRODUCT_ID` (`category_id`,`product_id`),
  ADD KEY `CAT_URL_REWRITE_PRD_CTGR_PRD_ID_CAT_PRD_ENTT_ENTT_ID` (`product_id`),
  ADD KEY `FK_BB79E64705D7F17FE181F23144528FC8` (`url_rewrite_id`);

--
-- Indexes for table `checkout_agreement`
--
ALTER TABLE `checkout_agreement`
  ADD PRIMARY KEY (`agreement_id`);

--
-- Indexes for table `checkout_agreement_store`
--
ALTER TABLE `checkout_agreement_store`
  ADD PRIMARY KEY (`agreement_id`,`store_id`),
  ADD KEY `CHECKOUT_AGREEMENT_STORE_STORE_ID_STORE_STORE_ID` (`store_id`);

--
-- Indexes for table `cms_block`
--
ALTER TABLE `cms_block`
  ADD PRIMARY KEY (`block_id`);
ALTER TABLE `cms_block` ADD FULLTEXT KEY `CMS_BLOCK_TITLE_IDENTIFIER_CONTENT` (`title`,`identifier`,`content`);

--
-- Indexes for table `cms_block_store`
--
ALTER TABLE `cms_block_store`
  ADD PRIMARY KEY (`block_id`,`store_id`),
  ADD KEY `CMS_BLOCK_STORE_STORE_ID` (`store_id`);

--
-- Indexes for table `cms_page`
--
ALTER TABLE `cms_page`
  ADD PRIMARY KEY (`page_id`),
  ADD KEY `CMS_PAGE_IDENTIFIER` (`identifier`);
ALTER TABLE `cms_page` ADD FULLTEXT KEY `CMS_PAGE_TITLE_META_KEYWORDS_META_DESCRIPTION_IDENTIFIER_CONTENT` (`title`,`meta_keywords`,`meta_description`,`identifier`,`content`);

--
-- Indexes for table `cms_page_store`
--
ALTER TABLE `cms_page_store`
  ADD PRIMARY KEY (`page_id`,`store_id`),
  ADD KEY `CMS_PAGE_STORE_STORE_ID` (`store_id`);

--
-- Indexes for table `core_config_data`
--
ALTER TABLE `core_config_data`
  ADD PRIMARY KEY (`config_id`),
  ADD UNIQUE KEY `CORE_CONFIG_DATA_SCOPE_SCOPE_ID_PATH` (`scope`,`scope_id`,`path`);

--
-- Indexes for table `cron_schedule`
--
ALTER TABLE `cron_schedule`
  ADD PRIMARY KEY (`schedule_id`),
  ADD KEY `CRON_SCHEDULE_JOB_CODE` (`job_code`),
  ADD KEY `CRON_SCHEDULE_SCHEDULED_AT_STATUS` (`scheduled_at`,`status`);

--
-- Indexes for table `customer_address_entity`
--
ALTER TABLE `customer_address_entity`
  ADD PRIMARY KEY (`entity_id`),
  ADD KEY `CUSTOMER_ADDRESS_ENTITY_PARENT_ID` (`parent_id`);

--
-- Indexes for table `customer_address_entity_datetime`
--
ALTER TABLE `customer_address_entity_datetime`
  ADD PRIMARY KEY (`value_id`),
  ADD UNIQUE KEY `CUSTOMER_ADDRESS_ENTITY_DATETIME_ENTITY_ID_ATTRIBUTE_ID` (`entity_id`,`attribute_id`),
  ADD KEY `CUSTOMER_ADDRESS_ENTITY_DATETIME_ATTRIBUTE_ID` (`attribute_id`),
  ADD KEY `CUSTOMER_ADDRESS_ENTITY_DATETIME_ENTITY_ID_ATTRIBUTE_ID_VALUE` (`entity_id`,`attribute_id`,`value`);

--
-- Indexes for table `customer_address_entity_decimal`
--
ALTER TABLE `customer_address_entity_decimal`
  ADD PRIMARY KEY (`value_id`),
  ADD UNIQUE KEY `CUSTOMER_ADDRESS_ENTITY_DECIMAL_ENTITY_ID_ATTRIBUTE_ID` (`entity_id`,`attribute_id`),
  ADD KEY `CUSTOMER_ADDRESS_ENTITY_DECIMAL_ATTRIBUTE_ID` (`attribute_id`),
  ADD KEY `CUSTOMER_ADDRESS_ENTITY_DECIMAL_ENTITY_ID_ATTRIBUTE_ID_VALUE` (`entity_id`,`attribute_id`,`value`);

--
-- Indexes for table `customer_address_entity_int`
--
ALTER TABLE `customer_address_entity_int`
  ADD PRIMARY KEY (`value_id`),
  ADD UNIQUE KEY `CUSTOMER_ADDRESS_ENTITY_INT_ENTITY_ID_ATTRIBUTE_ID` (`entity_id`,`attribute_id`),
  ADD KEY `CUSTOMER_ADDRESS_ENTITY_INT_ATTRIBUTE_ID` (`attribute_id`),
  ADD KEY `CUSTOMER_ADDRESS_ENTITY_INT_ENTITY_ID_ATTRIBUTE_ID_VALUE` (`entity_id`,`attribute_id`,`value`);

--
-- Indexes for table `customer_address_entity_text`
--
ALTER TABLE `customer_address_entity_text`
  ADD PRIMARY KEY (`value_id`),
  ADD UNIQUE KEY `CUSTOMER_ADDRESS_ENTITY_TEXT_ENTITY_ID_ATTRIBUTE_ID` (`entity_id`,`attribute_id`),
  ADD KEY `CUSTOMER_ADDRESS_ENTITY_TEXT_ATTRIBUTE_ID` (`attribute_id`);

--
-- Indexes for table `customer_address_entity_varchar`
--
ALTER TABLE `customer_address_entity_varchar`
  ADD PRIMARY KEY (`value_id`),
  ADD UNIQUE KEY `CUSTOMER_ADDRESS_ENTITY_VARCHAR_ENTITY_ID_ATTRIBUTE_ID` (`entity_id`,`attribute_id`),
  ADD KEY `CUSTOMER_ADDRESS_ENTITY_VARCHAR_ATTRIBUTE_ID` (`attribute_id`),
  ADD KEY `CUSTOMER_ADDRESS_ENTITY_VARCHAR_ENTITY_ID_ATTRIBUTE_ID_VALUE` (`entity_id`,`attribute_id`,`value`);

--
-- Indexes for table `customer_eav_attribute`
--
ALTER TABLE `customer_eav_attribute`
  ADD PRIMARY KEY (`attribute_id`);

--
-- Indexes for table `customer_eav_attribute_website`
--
ALTER TABLE `customer_eav_attribute_website`
  ADD PRIMARY KEY (`attribute_id`,`website_id`),
  ADD KEY `CUSTOMER_EAV_ATTRIBUTE_WEBSITE_WEBSITE_ID` (`website_id`);

--
-- Indexes for table `customer_entity`
--
ALTER TABLE `customer_entity`
  ADD PRIMARY KEY (`entity_id`),
  ADD UNIQUE KEY `CUSTOMER_ENTITY_EMAIL_WEBSITE_ID` (`email`,`website_id`),
  ADD KEY `CUSTOMER_ENTITY_STORE_ID` (`store_id`),
  ADD KEY `CUSTOMER_ENTITY_WEBSITE_ID` (`website_id`),
  ADD KEY `CUSTOMER_ENTITY_FIRSTNAME` (`firstname`),
  ADD KEY `CUSTOMER_ENTITY_LASTNAME` (`lastname`);

--
-- Indexes for table `customer_entity_datetime`
--
ALTER TABLE `customer_entity_datetime`
  ADD PRIMARY KEY (`value_id`),
  ADD UNIQUE KEY `CUSTOMER_ENTITY_DATETIME_ENTITY_ID_ATTRIBUTE_ID` (`entity_id`,`attribute_id`),
  ADD KEY `CUSTOMER_ENTITY_DATETIME_ATTRIBUTE_ID` (`attribute_id`),
  ADD KEY `CUSTOMER_ENTITY_DATETIME_ENTITY_ID_ATTRIBUTE_ID_VALUE` (`entity_id`,`attribute_id`,`value`);

--
-- Indexes for table `customer_entity_decimal`
--
ALTER TABLE `customer_entity_decimal`
  ADD PRIMARY KEY (`value_id`),
  ADD UNIQUE KEY `CUSTOMER_ENTITY_DECIMAL_ENTITY_ID_ATTRIBUTE_ID` (`entity_id`,`attribute_id`),
  ADD KEY `CUSTOMER_ENTITY_DECIMAL_ATTRIBUTE_ID` (`attribute_id`),
  ADD KEY `CUSTOMER_ENTITY_DECIMAL_ENTITY_ID_ATTRIBUTE_ID_VALUE` (`entity_id`,`attribute_id`,`value`);

--
-- Indexes for table `customer_entity_int`
--
ALTER TABLE `customer_entity_int`
  ADD PRIMARY KEY (`value_id`),
  ADD UNIQUE KEY `CUSTOMER_ENTITY_INT_ENTITY_ID_ATTRIBUTE_ID` (`entity_id`,`attribute_id`),
  ADD KEY `CUSTOMER_ENTITY_INT_ATTRIBUTE_ID` (`attribute_id`),
  ADD KEY `CUSTOMER_ENTITY_INT_ENTITY_ID_ATTRIBUTE_ID_VALUE` (`entity_id`,`attribute_id`,`value`);

--
-- Indexes for table `customer_entity_text`
--
ALTER TABLE `customer_entity_text`
  ADD PRIMARY KEY (`value_id`),
  ADD UNIQUE KEY `CUSTOMER_ENTITY_TEXT_ENTITY_ID_ATTRIBUTE_ID` (`entity_id`,`attribute_id`),
  ADD KEY `CUSTOMER_ENTITY_TEXT_ATTRIBUTE_ID` (`attribute_id`);

--
-- Indexes for table `customer_entity_varchar`
--
ALTER TABLE `customer_entity_varchar`
  ADD PRIMARY KEY (`value_id`),
  ADD UNIQUE KEY `CUSTOMER_ENTITY_VARCHAR_ENTITY_ID_ATTRIBUTE_ID` (`entity_id`,`attribute_id`),
  ADD KEY `CUSTOMER_ENTITY_VARCHAR_ATTRIBUTE_ID` (`attribute_id`),
  ADD KEY `CUSTOMER_ENTITY_VARCHAR_ENTITY_ID_ATTRIBUTE_ID_VALUE` (`entity_id`,`attribute_id`,`value`);

--
-- Indexes for table `customer_form_attribute`
--
ALTER TABLE `customer_form_attribute`
  ADD PRIMARY KEY (`form_code`,`attribute_id`),
  ADD KEY `CUSTOMER_FORM_ATTRIBUTE_ATTRIBUTE_ID` (`attribute_id`);

--
-- Indexes for table `customer_grid_flat`
--
ALTER TABLE `customer_grid_flat`
  ADD PRIMARY KEY (`entity_id`),
  ADD KEY `CUSTOMER_GRID_FLAT_GROUP_ID` (`group_id`),
  ADD KEY `CUSTOMER_GRID_FLAT_CREATED_AT` (`created_at`),
  ADD KEY `CUSTOMER_GRID_FLAT_WEBSITE_ID` (`website_id`),
  ADD KEY `CUSTOMER_GRID_FLAT_CONFIRMATION` (`confirmation`),
  ADD KEY `CUSTOMER_GRID_FLAT_DOB` (`dob`),
  ADD KEY `CUSTOMER_GRID_FLAT_GENDER` (`gender`),
  ADD KEY `CUSTOMER_GRID_FLAT_LAST_VISIT_AT` (`last_visit_at`),
  ADD KEY `CUSTOMER_GRID_FLAT_BILLING_COUNTRY_ID` (`billing_country_id`);
ALTER TABLE `customer_grid_flat` ADD FULLTEXT KEY `FTI_B691CA777399890C71AC8A4CDFB8EA99` (`name`,`email`,`created_in`,`taxvat`,`billing_full`,`billing_firstname`,`billing_lastname`,`billing_telephone`,`billing_postcode`,`billing_region`,`billing_city`,`billing_fax`,`billing_company`,`shipping_full`);

--
-- Indexes for table `customer_group`
--
ALTER TABLE `customer_group`
  ADD PRIMARY KEY (`customer_group_id`);

--
-- Indexes for table `customer_log`
--
ALTER TABLE `customer_log`
  ADD PRIMARY KEY (`log_id`),
  ADD UNIQUE KEY `CUSTOMER_LOG_CUSTOMER_ID` (`customer_id`);

--
-- Indexes for table `customer_visitor`
--
ALTER TABLE `customer_visitor`
  ADD PRIMARY KEY (`visitor_id`),
  ADD KEY `CUSTOMER_VISITOR_CUSTOMER_ID` (`customer_id`),
  ADD KEY `CUSTOMER_VISITOR_LAST_VISIT_AT` (`last_visit_at`);

--
-- Indexes for table `design_change`
--
ALTER TABLE `design_change`
  ADD PRIMARY KEY (`design_change_id`),
  ADD KEY `DESIGN_CHANGE_STORE_ID` (`store_id`);

--
-- Indexes for table `directory_country`
--
ALTER TABLE `directory_country`
  ADD PRIMARY KEY (`country_id`);

--
-- Indexes for table `directory_country_format`
--
ALTER TABLE `directory_country_format`
  ADD PRIMARY KEY (`country_format_id`),
  ADD UNIQUE KEY `DIRECTORY_COUNTRY_FORMAT_COUNTRY_ID_TYPE` (`country_id`,`type`);

--
-- Indexes for table `directory_country_region`
--
ALTER TABLE `directory_country_region`
  ADD PRIMARY KEY (`region_id`),
  ADD KEY `DIRECTORY_COUNTRY_REGION_COUNTRY_ID` (`country_id`);

--
-- Indexes for table `directory_country_region_name`
--
ALTER TABLE `directory_country_region_name`
  ADD PRIMARY KEY (`locale`,`region_id`),
  ADD KEY `DIRECTORY_COUNTRY_REGION_NAME_REGION_ID` (`region_id`);

--
-- Indexes for table `directory_currency_rate`
--
ALTER TABLE `directory_currency_rate`
  ADD PRIMARY KEY (`currency_from`,`currency_to`),
  ADD KEY `DIRECTORY_CURRENCY_RATE_CURRENCY_TO` (`currency_to`);

--
-- Indexes for table `downloadable_link`
--
ALTER TABLE `downloadable_link`
  ADD PRIMARY KEY (`link_id`),
  ADD KEY `DOWNLOADABLE_LINK_PRODUCT_ID_SORT_ORDER` (`product_id`,`sort_order`);

--
-- Indexes for table `downloadable_link_price`
--
ALTER TABLE `downloadable_link_price`
  ADD PRIMARY KEY (`price_id`),
  ADD KEY `DOWNLOADABLE_LINK_PRICE_LINK_ID` (`link_id`),
  ADD KEY `DOWNLOADABLE_LINK_PRICE_WEBSITE_ID` (`website_id`);

--
-- Indexes for table `downloadable_link_purchased`
--
ALTER TABLE `downloadable_link_purchased`
  ADD PRIMARY KEY (`purchased_id`),
  ADD KEY `DOWNLOADABLE_LINK_PURCHASED_ORDER_ID` (`order_id`),
  ADD KEY `DOWNLOADABLE_LINK_PURCHASED_ORDER_ITEM_ID` (`order_item_id`),
  ADD KEY `DOWNLOADABLE_LINK_PURCHASED_CUSTOMER_ID` (`customer_id`);

--
-- Indexes for table `downloadable_link_purchased_item`
--
ALTER TABLE `downloadable_link_purchased_item`
  ADD PRIMARY KEY (`item_id`),
  ADD KEY `DOWNLOADABLE_LINK_PURCHASED_ITEM_LINK_HASH` (`link_hash`),
  ADD KEY `DOWNLOADABLE_LINK_PURCHASED_ITEM_ORDER_ITEM_ID` (`order_item_id`),
  ADD KEY `DOWNLOADABLE_LINK_PURCHASED_ITEM_PURCHASED_ID` (`purchased_id`);

--
-- Indexes for table `downloadable_link_title`
--
ALTER TABLE `downloadable_link_title`
  ADD PRIMARY KEY (`title_id`),
  ADD UNIQUE KEY `DOWNLOADABLE_LINK_TITLE_LINK_ID_STORE_ID` (`link_id`,`store_id`),
  ADD KEY `DOWNLOADABLE_LINK_TITLE_STORE_ID` (`store_id`);

--
-- Indexes for table `downloadable_sample`
--
ALTER TABLE `downloadable_sample`
  ADD PRIMARY KEY (`sample_id`),
  ADD KEY `DOWNLOADABLE_SAMPLE_PRODUCT_ID` (`product_id`);

--
-- Indexes for table `downloadable_sample_title`
--
ALTER TABLE `downloadable_sample_title`
  ADD PRIMARY KEY (`title_id`),
  ADD UNIQUE KEY `DOWNLOADABLE_SAMPLE_TITLE_SAMPLE_ID_STORE_ID` (`sample_id`,`store_id`),
  ADD KEY `DOWNLOADABLE_SAMPLE_TITLE_STORE_ID` (`store_id`);

--
-- Indexes for table `eav_attribute`
--
ALTER TABLE `eav_attribute`
  ADD PRIMARY KEY (`attribute_id`),
  ADD UNIQUE KEY `EAV_ATTRIBUTE_ENTITY_TYPE_ID_ATTRIBUTE_CODE` (`entity_type_id`,`attribute_code`);

--
-- Indexes for table `eav_attribute_group`
--
ALTER TABLE `eav_attribute_group`
  ADD PRIMARY KEY (`attribute_group_id`),
  ADD UNIQUE KEY `EAV_ATTRIBUTE_GROUP_ATTRIBUTE_SET_ID_ATTRIBUTE_GROUP_NAME` (`attribute_set_id`,`attribute_group_name`),
  ADD KEY `EAV_ATTRIBUTE_GROUP_ATTRIBUTE_SET_ID_SORT_ORDER` (`attribute_set_id`,`sort_order`);

--
-- Indexes for table `eav_attribute_label`
--
ALTER TABLE `eav_attribute_label`
  ADD PRIMARY KEY (`attribute_label_id`),
  ADD KEY `EAV_ATTRIBUTE_LABEL_STORE_ID` (`store_id`),
  ADD KEY `EAV_ATTRIBUTE_LABEL_ATTRIBUTE_ID_STORE_ID` (`attribute_id`,`store_id`);

--
-- Indexes for table `eav_attribute_option`
--
ALTER TABLE `eav_attribute_option`
  ADD PRIMARY KEY (`option_id`),
  ADD KEY `EAV_ATTRIBUTE_OPTION_ATTRIBUTE_ID` (`attribute_id`);

--
-- Indexes for table `eav_attribute_option_swatch`
--
ALTER TABLE `eav_attribute_option_swatch`
  ADD PRIMARY KEY (`swatch_id`),
  ADD UNIQUE KEY `EAV_ATTRIBUTE_OPTION_SWATCH_STORE_ID_OPTION_ID` (`store_id`,`option_id`),
  ADD KEY `EAV_ATTRIBUTE_OPTION_SWATCH_SWATCH_ID` (`swatch_id`),
  ADD KEY `EAV_ATTR_OPT_SWATCH_OPT_ID_EAV_ATTR_OPT_OPT_ID` (`option_id`);

--
-- Indexes for table `eav_attribute_option_value`
--
ALTER TABLE `eav_attribute_option_value`
  ADD PRIMARY KEY (`value_id`),
  ADD KEY `EAV_ATTRIBUTE_OPTION_VALUE_OPTION_ID` (`option_id`),
  ADD KEY `EAV_ATTRIBUTE_OPTION_VALUE_STORE_ID` (`store_id`);

--
-- Indexes for table `eav_attribute_set`
--
ALTER TABLE `eav_attribute_set`
  ADD PRIMARY KEY (`attribute_set_id`),
  ADD UNIQUE KEY `EAV_ATTRIBUTE_SET_ENTITY_TYPE_ID_ATTRIBUTE_SET_NAME` (`entity_type_id`,`attribute_set_name`),
  ADD KEY `EAV_ATTRIBUTE_SET_ENTITY_TYPE_ID_SORT_ORDER` (`entity_type_id`,`sort_order`);

--
-- Indexes for table `eav_entity`
--
ALTER TABLE `eav_entity`
  ADD PRIMARY KEY (`entity_id`),
  ADD KEY `EAV_ENTITY_ENTITY_TYPE_ID` (`entity_type_id`),
  ADD KEY `EAV_ENTITY_STORE_ID` (`store_id`);

--
-- Indexes for table `eav_entity_attribute`
--
ALTER TABLE `eav_entity_attribute`
  ADD PRIMARY KEY (`entity_attribute_id`),
  ADD UNIQUE KEY `EAV_ENTITY_ATTRIBUTE_ATTRIBUTE_SET_ID_ATTRIBUTE_ID` (`attribute_set_id`,`attribute_id`),
  ADD UNIQUE KEY `EAV_ENTITY_ATTRIBUTE_ATTRIBUTE_GROUP_ID_ATTRIBUTE_ID` (`attribute_group_id`,`attribute_id`),
  ADD KEY `EAV_ENTITY_ATTRIBUTE_ATTRIBUTE_SET_ID_SORT_ORDER` (`attribute_set_id`,`sort_order`),
  ADD KEY `EAV_ENTITY_ATTRIBUTE_ATTRIBUTE_ID` (`attribute_id`);

--
-- Indexes for table `eav_entity_datetime`
--
ALTER TABLE `eav_entity_datetime`
  ADD PRIMARY KEY (`value_id`),
  ADD UNIQUE KEY `EAV_ENTITY_DATETIME_ENTITY_ID_ATTRIBUTE_ID_STORE_ID` (`entity_id`,`attribute_id`,`store_id`),
  ADD KEY `EAV_ENTITY_DATETIME_STORE_ID` (`store_id`),
  ADD KEY `EAV_ENTITY_DATETIME_ATTRIBUTE_ID_VALUE` (`attribute_id`,`value`),
  ADD KEY `EAV_ENTITY_DATETIME_ENTITY_TYPE_ID_VALUE` (`entity_type_id`,`value`);

--
-- Indexes for table `eav_entity_decimal`
--
ALTER TABLE `eav_entity_decimal`
  ADD PRIMARY KEY (`value_id`),
  ADD UNIQUE KEY `EAV_ENTITY_DECIMAL_ENTITY_ID_ATTRIBUTE_ID_STORE_ID` (`entity_id`,`attribute_id`,`store_id`),
  ADD KEY `EAV_ENTITY_DECIMAL_STORE_ID` (`store_id`),
  ADD KEY `EAV_ENTITY_DECIMAL_ATTRIBUTE_ID_VALUE` (`attribute_id`,`value`),
  ADD KEY `EAV_ENTITY_DECIMAL_ENTITY_TYPE_ID_VALUE` (`entity_type_id`,`value`);

--
-- Indexes for table `eav_entity_int`
--
ALTER TABLE `eav_entity_int`
  ADD PRIMARY KEY (`value_id`),
  ADD UNIQUE KEY `EAV_ENTITY_INT_ENTITY_ID_ATTRIBUTE_ID_STORE_ID` (`entity_id`,`attribute_id`,`store_id`),
  ADD KEY `EAV_ENTITY_INT_STORE_ID` (`store_id`),
  ADD KEY `EAV_ENTITY_INT_ATTRIBUTE_ID_VALUE` (`attribute_id`,`value`),
  ADD KEY `EAV_ENTITY_INT_ENTITY_TYPE_ID_VALUE` (`entity_type_id`,`value`);

--
-- Indexes for table `eav_entity_store`
--
ALTER TABLE `eav_entity_store`
  ADD PRIMARY KEY (`entity_store_id`),
  ADD KEY `EAV_ENTITY_STORE_ENTITY_TYPE_ID` (`entity_type_id`),
  ADD KEY `EAV_ENTITY_STORE_STORE_ID` (`store_id`);

--
-- Indexes for table `eav_entity_text`
--
ALTER TABLE `eav_entity_text`
  ADD PRIMARY KEY (`value_id`),
  ADD UNIQUE KEY `EAV_ENTITY_TEXT_ENTITY_ID_ATTRIBUTE_ID_STORE_ID` (`entity_id`,`attribute_id`,`store_id`),
  ADD KEY `EAV_ENTITY_TEXT_ENTITY_TYPE_ID` (`entity_type_id`),
  ADD KEY `EAV_ENTITY_TEXT_ATTRIBUTE_ID` (`attribute_id`),
  ADD KEY `EAV_ENTITY_TEXT_STORE_ID` (`store_id`);

--
-- Indexes for table `eav_entity_type`
--
ALTER TABLE `eav_entity_type`
  ADD PRIMARY KEY (`entity_type_id`),
  ADD KEY `EAV_ENTITY_TYPE_ENTITY_TYPE_CODE` (`entity_type_code`);

--
-- Indexes for table `eav_entity_varchar`
--
ALTER TABLE `eav_entity_varchar`
  ADD PRIMARY KEY (`value_id`),
  ADD UNIQUE KEY `EAV_ENTITY_VARCHAR_ENTITY_ID_ATTRIBUTE_ID_STORE_ID` (`entity_id`,`attribute_id`,`store_id`),
  ADD KEY `EAV_ENTITY_VARCHAR_STORE_ID` (`store_id`),
  ADD KEY `EAV_ENTITY_VARCHAR_ATTRIBUTE_ID_VALUE` (`attribute_id`,`value`),
  ADD KEY `EAV_ENTITY_VARCHAR_ENTITY_TYPE_ID_VALUE` (`entity_type_id`,`value`);

--
-- Indexes for table `eav_form_element`
--
ALTER TABLE `eav_form_element`
  ADD PRIMARY KEY (`element_id`),
  ADD UNIQUE KEY `EAV_FORM_ELEMENT_TYPE_ID_ATTRIBUTE_ID` (`type_id`,`attribute_id`),
  ADD KEY `EAV_FORM_ELEMENT_FIELDSET_ID` (`fieldset_id`),
  ADD KEY `EAV_FORM_ELEMENT_ATTRIBUTE_ID` (`attribute_id`);

--
-- Indexes for table `eav_form_fieldset`
--
ALTER TABLE `eav_form_fieldset`
  ADD PRIMARY KEY (`fieldset_id`),
  ADD UNIQUE KEY `EAV_FORM_FIELDSET_TYPE_ID_CODE` (`type_id`,`code`);

--
-- Indexes for table `eav_form_fieldset_label`
--
ALTER TABLE `eav_form_fieldset_label`
  ADD PRIMARY KEY (`fieldset_id`,`store_id`),
  ADD KEY `EAV_FORM_FIELDSET_LABEL_STORE_ID` (`store_id`);

--
-- Indexes for table `eav_form_type`
--
ALTER TABLE `eav_form_type`
  ADD PRIMARY KEY (`type_id`),
  ADD UNIQUE KEY `EAV_FORM_TYPE_CODE_THEME_STORE_ID` (`code`,`theme`,`store_id`),
  ADD KEY `EAV_FORM_TYPE_STORE_ID` (`store_id`);

--
-- Indexes for table `eav_form_type_entity`
--
ALTER TABLE `eav_form_type_entity`
  ADD PRIMARY KEY (`type_id`,`entity_type_id`),
  ADD KEY `EAV_FORM_TYPE_ENTITY_ENTITY_TYPE_ID` (`entity_type_id`);

--
-- Indexes for table `email_template`
--
ALTER TABLE `email_template`
  ADD PRIMARY KEY (`template_id`),
  ADD UNIQUE KEY `EMAIL_TEMPLATE_TEMPLATE_CODE` (`template_code`),
  ADD KEY `EMAIL_TEMPLATE_ADDED_AT` (`added_at`),
  ADD KEY `EMAIL_TEMPLATE_MODIFIED_AT` (`modified_at`);

--
-- Indexes for table `flag`
--
ALTER TABLE `flag`
  ADD PRIMARY KEY (`flag_id`),
  ADD KEY `FLAG_LAST_UPDATE` (`last_update`);

--
-- Indexes for table `gift_message`
--
ALTER TABLE `gift_message`
  ADD PRIMARY KEY (`gift_message_id`);

--
-- Indexes for table `googleoptimizer_code`
--
ALTER TABLE `googleoptimizer_code`
  ADD PRIMARY KEY (`code_id`),
  ADD UNIQUE KEY `GOOGLEOPTIMIZER_CODE_STORE_ID_ENTITY_ID_ENTITY_TYPE` (`store_id`,`entity_id`,`entity_type`);

--
-- Indexes for table `importexport_importdata`
--
ALTER TABLE `importexport_importdata`
  ADD PRIMARY KEY (`id`);

--
-- Indexes for table `import_history`
--
ALTER TABLE `import_history`
  ADD PRIMARY KEY (`history_id`);

--
-- Indexes for table `indexer_state`
--
ALTER TABLE `indexer_state`
  ADD PRIMARY KEY (`state_id`),
  ADD KEY `INDEXER_STATE_INDEXER_ID` (`indexer_id`);

--
-- Indexes for table `integration`
--
ALTER TABLE `integration`
  ADD PRIMARY KEY (`integration_id`),
  ADD UNIQUE KEY `INTEGRATION_NAME` (`name`),
  ADD UNIQUE KEY `INTEGRATION_CONSUMER_ID` (`consumer_id`);

--
-- Indexes for table `layout_link`
--
ALTER TABLE `layout_link`
  ADD PRIMARY KEY (`layout_link_id`),
  ADD KEY `LAYOUT_LINK_LAYOUT_UPDATE_ID` (`layout_update_id`),
  ADD KEY `LAYOUT_LINK_STORE_ID_THEME_ID_LAYOUT_UPDATE_ID_IS_TEMPORARY` (`store_id`,`theme_id`,`layout_update_id`,`is_temporary`),
  ADD KEY `LAYOUT_LINK_THEME_ID_THEME_THEME_ID` (`theme_id`);

--
-- Indexes for table `layout_update`
--
ALTER TABLE `layout_update`
  ADD PRIMARY KEY (`layout_update_id`),
  ADD KEY `LAYOUT_UPDATE_HANDLE` (`handle`);

--
-- Indexes for table `mview_state`
--
ALTER TABLE `mview_state`
  ADD PRIMARY KEY (`state_id`),
  ADD KEY `MVIEW_STATE_VIEW_ID` (`view_id`),
  ADD KEY `MVIEW_STATE_MODE` (`mode`);

--
-- Indexes for table `newsletter_problem`
--
ALTER TABLE `newsletter_problem`
  ADD PRIMARY KEY (`problem_id`),
  ADD KEY `NEWSLETTER_PROBLEM_SUBSCRIBER_ID` (`subscriber_id`),
  ADD KEY `NEWSLETTER_PROBLEM_QUEUE_ID` (`queue_id`);

--
-- Indexes for table `newsletter_queue`
--
ALTER TABLE `newsletter_queue`
  ADD PRIMARY KEY (`queue_id`),
  ADD KEY `NEWSLETTER_QUEUE_TEMPLATE_ID` (`template_id`);

--
-- Indexes for table `newsletter_queue_link`
--
ALTER TABLE `newsletter_queue_link`
  ADD PRIMARY KEY (`queue_link_id`),
  ADD KEY `NEWSLETTER_QUEUE_LINK_SUBSCRIBER_ID` (`subscriber_id`),
  ADD KEY `NEWSLETTER_QUEUE_LINK_QUEUE_ID_LETTER_SENT_AT` (`queue_id`,`letter_sent_at`);

--
-- Indexes for table `newsletter_queue_store_link`
--
ALTER TABLE `newsletter_queue_store_link`
  ADD PRIMARY KEY (`queue_id`,`store_id`),
  ADD KEY `NEWSLETTER_QUEUE_STORE_LINK_STORE_ID` (`store_id`);

--
-- Indexes for table `newsletter_subscriber`
--
ALTER TABLE `newsletter_subscriber`
  ADD PRIMARY KEY (`subscriber_id`),
  ADD KEY `NEWSLETTER_SUBSCRIBER_CUSTOMER_ID` (`customer_id`),
  ADD KEY `NEWSLETTER_SUBSCRIBER_STORE_ID` (`store_id`);

--
-- Indexes for table `newsletter_template`
--
ALTER TABLE `newsletter_template`
  ADD PRIMARY KEY (`template_id`),
  ADD KEY `NEWSLETTER_TEMPLATE_TEMPLATE_ACTUAL` (`template_actual`),
  ADD KEY `NEWSLETTER_TEMPLATE_ADDED_AT` (`added_at`),
  ADD KEY `NEWSLETTER_TEMPLATE_MODIFIED_AT` (`modified_at`);

--
-- Indexes for table `oauth_consumer`
--
ALTER TABLE `oauth_consumer`
  ADD PRIMARY KEY (`entity_id`),
  ADD UNIQUE KEY `OAUTH_CONSUMER_KEY` (`key`),
  ADD UNIQUE KEY `OAUTH_CONSUMER_SECRET` (`secret`),
  ADD KEY `OAUTH_CONSUMER_CREATED_AT` (`created_at`),
  ADD KEY `OAUTH_CONSUMER_UPDATED_AT` (`updated_at`);

--
-- Indexes for table `oauth_nonce`
--
ALTER TABLE `oauth_nonce`
  ADD UNIQUE KEY `OAUTH_NONCE_NONCE_CONSUMER_ID` (`nonce`,`consumer_id`),
  ADD KEY `OAUTH_NONCE_CONSUMER_ID_OAUTH_CONSUMER_ENTITY_ID` (`consumer_id`);

--
-- Indexes for table `oauth_token`
--
ALTER TABLE `oauth_token`
  ADD PRIMARY KEY (`entity_id`),
  ADD UNIQUE KEY `OAUTH_TOKEN_TOKEN` (`token`),
  ADD KEY `OAUTH_TOKEN_CONSUMER_ID` (`consumer_id`),
  ADD KEY `OAUTH_TOKEN_ADMIN_ID_ADMIN_USER_USER_ID` (`admin_id`),
  ADD KEY `OAUTH_TOKEN_CUSTOMER_ID_CUSTOMER_ENTITY_ENTITY_ID` (`customer_id`);

--
-- Indexes for table `oauth_token_request_log`
--
ALTER TABLE `oauth_token_request_log`
  ADD PRIMARY KEY (`log_id`),
  ADD UNIQUE KEY `OAUTH_TOKEN_REQUEST_LOG_USER_NAME_USER_TYPE` (`user_name`,`user_type`);

--
-- Indexes for table `paypal_billing_agreement`
--
ALTER TABLE `paypal_billing_agreement`
  ADD PRIMARY KEY (`agreement_id`),
  ADD KEY `PAYPAL_BILLING_AGREEMENT_CUSTOMER_ID` (`customer_id`),
  ADD KEY `PAYPAL_BILLING_AGREEMENT_STORE_ID` (`store_id`);

--
-- Indexes for table `paypal_billing_agreement_order`
--
ALTER TABLE `paypal_billing_agreement_order`
  ADD PRIMARY KEY (`agreement_id`,`order_id`),
  ADD KEY `PAYPAL_BILLING_AGREEMENT_ORDER_ORDER_ID` (`order_id`);

--
-- Indexes for table `paypal_cert`
--
ALTER TABLE `paypal_cert`
  ADD PRIMARY KEY (`cert_id`),
  ADD KEY `PAYPAL_CERT_WEBSITE_ID` (`website_id`);

--
-- Indexes for table `paypal_payment_transaction`
--
ALTER TABLE `paypal_payment_transaction`
  ADD PRIMARY KEY (`transaction_id`),
  ADD UNIQUE KEY `PAYPAL_PAYMENT_TRANSACTION_TXN_ID` (`txn_id`);

--
-- Indexes for table `paypal_settlement_report`
--
ALTER TABLE `paypal_settlement_report`
  ADD PRIMARY KEY (`report_id`),
  ADD UNIQUE KEY `PAYPAL_SETTLEMENT_REPORT_REPORT_DATE_ACCOUNT_ID` (`report_date`,`account_id`);

--
-- Indexes for table `paypal_settlement_report_row`
--
ALTER TABLE `paypal_settlement_report_row`
  ADD PRIMARY KEY (`row_id`),
  ADD KEY `PAYPAL_SETTLEMENT_REPORT_ROW_REPORT_ID` (`report_id`);

--
-- Indexes for table `persistent_session`
--
ALTER TABLE `persistent_session`
  ADD PRIMARY KEY (`persistent_id`),
  ADD UNIQUE KEY `PERSISTENT_SESSION_KEY` (`key`),
  ADD UNIQUE KEY `PERSISTENT_SESSION_CUSTOMER_ID` (`customer_id`),
  ADD KEY `PERSISTENT_SESSION_UPDATED_AT` (`updated_at`),
  ADD KEY `PERSISTENT_SESSION_WEBSITE_ID_STORE_WEBSITE_WEBSITE_ID` (`website_id`);

--
-- Indexes for table `product_alert_price`
--
ALTER TABLE `product_alert_price`
  ADD PRIMARY KEY (`alert_price_id`),
  ADD KEY `PRODUCT_ALERT_PRICE_CUSTOMER_ID` (`customer_id`),
  ADD KEY `PRODUCT_ALERT_PRICE_PRODUCT_ID` (`product_id`),
  ADD KEY `PRODUCT_ALERT_PRICE_WEBSITE_ID` (`website_id`);

--
-- Indexes for table `product_alert_stock`
--
ALTER TABLE `product_alert_stock`
  ADD PRIMARY KEY (`alert_stock_id`),
  ADD KEY `PRODUCT_ALERT_STOCK_CUSTOMER_ID` (`customer_id`),
  ADD KEY `PRODUCT_ALERT_STOCK_PRODUCT_ID` (`product_id`),
  ADD KEY `PRODUCT_ALERT_STOCK_WEBSITE_ID` (`website_id`);

--
-- Indexes for table `quote`
--
ALTER TABLE `quote`
  ADD PRIMARY KEY (`entity_id`),
  ADD KEY `QUOTE_CUSTOMER_ID_STORE_ID_IS_ACTIVE` (`customer_id`,`store_id`,`is_active`),
  ADD KEY `QUOTE_STORE_ID` (`store_id`);

--
-- Indexes for table `quote_address`
--
ALTER TABLE `quote_address`
  ADD PRIMARY KEY (`address_id`),
  ADD KEY `QUOTE_ADDRESS_QUOTE_ID` (`quote_id`);

--
-- Indexes for table `quote_address_item`
--
ALTER TABLE `quote_address_item`
  ADD PRIMARY KEY (`address_item_id`),
  ADD KEY `QUOTE_ADDRESS_ITEM_QUOTE_ADDRESS_ID` (`quote_address_id`),
  ADD KEY `QUOTE_ADDRESS_ITEM_PARENT_ITEM_ID` (`parent_item_id`),
  ADD KEY `QUOTE_ADDRESS_ITEM_QUOTE_ITEM_ID` (`quote_item_id`);

--
-- Indexes for table `quote_id_mask`
--
ALTER TABLE `quote_id_mask`
  ADD PRIMARY KEY (`entity_id`,`quote_id`),
  ADD KEY `QUOTE_ID_MASK_QUOTE_ID` (`quote_id`),
  ADD KEY `QUOTE_ID_MASK_MASKED_ID` (`masked_id`);

--
-- Indexes for table `quote_item`
--
ALTER TABLE `quote_item`
  ADD PRIMARY KEY (`item_id`),
  ADD KEY `QUOTE_ITEM_PARENT_ITEM_ID` (`parent_item_id`),
  ADD KEY `QUOTE_ITEM_PRODUCT_ID` (`product_id`),
  ADD KEY `QUOTE_ITEM_QUOTE_ID` (`quote_id`),
  ADD KEY `QUOTE_ITEM_STORE_ID` (`store_id`);

--
-- Indexes for table `quote_item_option`
--
ALTER TABLE `quote_item_option`
  ADD PRIMARY KEY (`option_id`),
  ADD KEY `QUOTE_ITEM_OPTION_ITEM_ID` (`item_id`);

--
-- Indexes for table `quote_payment`
--
ALTER TABLE `quote_payment`
  ADD PRIMARY KEY (`payment_id`),
  ADD KEY `QUOTE_PAYMENT_QUOTE_ID` (`quote_id`);

--
-- Indexes for table `quote_shipping_rate`
--
ALTER TABLE `quote_shipping_rate`
  ADD PRIMARY KEY (`rate_id`),
  ADD KEY `QUOTE_SHIPPING_RATE_ADDRESS_ID` (`address_id`);

--
-- Indexes for table `rating`
--
ALTER TABLE `rating`
  ADD PRIMARY KEY (`rating_id`),
  ADD UNIQUE KEY `RATING_RATING_CODE` (`rating_code`),
  ADD KEY `RATING_ENTITY_ID` (`entity_id`);

--
-- Indexes for table `rating_entity`
--
ALTER TABLE `rating_entity`
  ADD PRIMARY KEY (`entity_id`),
  ADD UNIQUE KEY `RATING_ENTITY_ENTITY_CODE` (`entity_code`);

--
-- Indexes for table `rating_option`
--
ALTER TABLE `rating_option`
  ADD PRIMARY KEY (`option_id`),
  ADD KEY `RATING_OPTION_RATING_ID` (`rating_id`);

--
-- Indexes for table `rating_option_vote`
--
ALTER TABLE `rating_option_vote`
  ADD PRIMARY KEY (`vote_id`),
  ADD KEY `RATING_OPTION_VOTE_OPTION_ID` (`option_id`),
  ADD KEY `RATING_OPTION_VOTE_REVIEW_ID_REVIEW_REVIEW_ID` (`review_id`);

--
-- Indexes for table `rating_option_vote_aggregated`
--
ALTER TABLE `rating_option_vote_aggregated`
  ADD PRIMARY KEY (`primary_id`),
  ADD KEY `RATING_OPTION_VOTE_AGGREGATED_RATING_ID` (`rating_id`),
  ADD KEY `RATING_OPTION_VOTE_AGGREGATED_STORE_ID` (`store_id`);

--
-- Indexes for table `rating_store`
--
ALTER TABLE `rating_store`
  ADD PRIMARY KEY (`rating_id`,`store_id`),
  ADD KEY `RATING_STORE_STORE_ID` (`store_id`);

--
-- Indexes for table `rating_title`
--
ALTER TABLE `rating_title`
  ADD PRIMARY KEY (`rating_id`,`store_id`),
  ADD KEY `RATING_TITLE_STORE_ID` (`store_id`);

--
-- Indexes for table `reporting_counts`
--
ALTER TABLE `reporting_counts`
  ADD PRIMARY KEY (`entity_id`);

--
-- Indexes for table `reporting_module_status`
--
ALTER TABLE `reporting_module_status`
  ADD PRIMARY KEY (`entity_id`);

--
-- Indexes for table `reporting_orders`
--
ALTER TABLE `reporting_orders`
  ADD PRIMARY KEY (`entity_id`);

--
-- Indexes for table `reporting_system_updates`
--
ALTER TABLE `reporting_system_updates`
  ADD PRIMARY KEY (`entity_id`);

--
-- Indexes for table `reporting_users`
--
ALTER TABLE `reporting_users`
  ADD PRIMARY KEY (`entity_id`);

--
-- Indexes for table `report_compared_product_index`
--
ALTER TABLE `report_compared_product_index`
  ADD PRIMARY KEY (`index_id`),
  ADD UNIQUE KEY `REPORT_COMPARED_PRODUCT_INDEX_VISITOR_ID_PRODUCT_ID` (`visitor_id`,`product_id`),
  ADD UNIQUE KEY `REPORT_COMPARED_PRODUCT_INDEX_CUSTOMER_ID_PRODUCT_ID` (`customer_id`,`product_id`),
  ADD KEY `REPORT_COMPARED_PRODUCT_INDEX_STORE_ID` (`store_id`),
  ADD KEY `REPORT_COMPARED_PRODUCT_INDEX_ADDED_AT` (`added_at`),
  ADD KEY `REPORT_COMPARED_PRODUCT_INDEX_PRODUCT_ID` (`product_id`);

--
-- Indexes for table `report_event`
--
ALTER TABLE `report_event`
  ADD PRIMARY KEY (`event_id`),
  ADD KEY `REPORT_EVENT_EVENT_TYPE_ID` (`event_type_id`),
  ADD KEY `REPORT_EVENT_SUBJECT_ID` (`subject_id`),
  ADD KEY `REPORT_EVENT_OBJECT_ID` (`object_id`),
  ADD KEY `REPORT_EVENT_SUBTYPE` (`subtype`),
  ADD KEY `REPORT_EVENT_STORE_ID` (`store_id`);

--
-- Indexes for table `report_event_types`
--
ALTER TABLE `report_event_types`
  ADD PRIMARY KEY (`event_type_id`);

--
-- Indexes for table `report_viewed_product_aggregated_daily`
--
ALTER TABLE `report_viewed_product_aggregated_daily`
  ADD PRIMARY KEY (`id`),
  ADD UNIQUE KEY `REPORT_VIEWED_PRD_AGGRED_DAILY_PERIOD_STORE_ID_PRD_ID` (`period`,`store_id`,`product_id`),
  ADD KEY `REPORT_VIEWED_PRODUCT_AGGREGATED_DAILY_STORE_ID` (`store_id`),
  ADD KEY `REPORT_VIEWED_PRODUCT_AGGREGATED_DAILY_PRODUCT_ID` (`product_id`);

--
-- Indexes for table `report_viewed_product_aggregated_monthly`
--
ALTER TABLE `report_viewed_product_aggregated_monthly`
  ADD PRIMARY KEY (`id`),
  ADD UNIQUE KEY `REPORT_VIEWED_PRD_AGGRED_MONTHLY_PERIOD_STORE_ID_PRD_ID` (`period`,`store_id`,`product_id`),
  ADD KEY `REPORT_VIEWED_PRODUCT_AGGREGATED_MONTHLY_STORE_ID` (`store_id`),
  ADD KEY `REPORT_VIEWED_PRODUCT_AGGREGATED_MONTHLY_PRODUCT_ID` (`product_id`);

--
-- Indexes for table `report_viewed_product_aggregated_yearly`
--
ALTER TABLE `report_viewed_product_aggregated_yearly`
  ADD PRIMARY KEY (`id`),
  ADD UNIQUE KEY `REPORT_VIEWED_PRD_AGGRED_YEARLY_PERIOD_STORE_ID_PRD_ID` (`period`,`store_id`,`product_id`),
  ADD KEY `REPORT_VIEWED_PRODUCT_AGGREGATED_YEARLY_STORE_ID` (`store_id`),
  ADD KEY `REPORT_VIEWED_PRODUCT_AGGREGATED_YEARLY_PRODUCT_ID` (`product_id`);

--
-- Indexes for table `report_viewed_product_index`
--
ALTER TABLE `report_viewed_product_index`
  ADD PRIMARY KEY (`index_id`),
  ADD UNIQUE KEY `REPORT_VIEWED_PRODUCT_INDEX_VISITOR_ID_PRODUCT_ID` (`visitor_id`,`product_id`),
  ADD UNIQUE KEY `REPORT_VIEWED_PRODUCT_INDEX_CUSTOMER_ID_PRODUCT_ID` (`customer_id`,`product_id`),
  ADD KEY `REPORT_VIEWED_PRODUCT_INDEX_STORE_ID` (`store_id`),
  ADD KEY `REPORT_VIEWED_PRODUCT_INDEX_ADDED_AT` (`added_at`),
  ADD KEY `REPORT_VIEWED_PRODUCT_INDEX_PRODUCT_ID` (`product_id`);

--
-- Indexes for table `review`
--
ALTER TABLE `review`
  ADD PRIMARY KEY (`review_id`),
  ADD KEY `REVIEW_ENTITY_ID` (`entity_id`),
  ADD KEY `REVIEW_STATUS_ID` (`status_id`),
  ADD KEY `REVIEW_ENTITY_PK_VALUE` (`entity_pk_value`);

--
-- Indexes for table `review_detail`
--
ALTER TABLE `review_detail`
  ADD PRIMARY KEY (`detail_id`),
  ADD KEY `REVIEW_DETAIL_REVIEW_ID` (`review_id`),
  ADD KEY `REVIEW_DETAIL_STORE_ID` (`store_id`),
  ADD KEY `REVIEW_DETAIL_CUSTOMER_ID` (`customer_id`);

--
-- Indexes for table `review_entity`
--
ALTER TABLE `review_entity`
  ADD PRIMARY KEY (`entity_id`);

--
-- Indexes for table `review_entity_summary`
--
ALTER TABLE `review_entity_summary`
  ADD PRIMARY KEY (`primary_id`),
  ADD KEY `REVIEW_ENTITY_SUMMARY_STORE_ID` (`store_id`);

--
-- Indexes for table `review_status`
--
ALTER TABLE `review_status`
  ADD PRIMARY KEY (`status_id`);

--
-- Indexes for table `review_store`
--
ALTER TABLE `review_store`
  ADD PRIMARY KEY (`review_id`,`store_id`),
  ADD KEY `REVIEW_STORE_STORE_ID` (`store_id`);

--
-- Indexes for table `salesrule`
--
ALTER TABLE `salesrule`
  ADD PRIMARY KEY (`rule_id`),
  ADD KEY `SALESRULE_IS_ACTIVE_SORT_ORDER_TO_DATE_FROM_DATE` (`is_active`,`sort_order`,`to_date`,`from_date`);

--
-- Indexes for table `salesrule_coupon`
--
ALTER TABLE `salesrule_coupon`
  ADD PRIMARY KEY (`coupon_id`),
  ADD UNIQUE KEY `SALESRULE_COUPON_CODE` (`code`),
  ADD UNIQUE KEY `SALESRULE_COUPON_RULE_ID_IS_PRIMARY` (`rule_id`,`is_primary`),
  ADD KEY `SALESRULE_COUPON_RULE_ID` (`rule_id`);

--
-- Indexes for table `salesrule_coupon_aggregated`
--
ALTER TABLE `salesrule_coupon_aggregated`
  ADD PRIMARY KEY (`id`),
  ADD UNIQUE KEY `SALESRULE_COUPON_AGGRED_PERIOD_STORE_ID_ORDER_STS_COUPON_CODE` (`period`,`store_id`,`order_status`,`coupon_code`),
  ADD KEY `SALESRULE_COUPON_AGGREGATED_STORE_ID` (`store_id`),
  ADD KEY `SALESRULE_COUPON_AGGREGATED_RULE_NAME` (`rule_name`);

--
-- Indexes for table `salesrule_coupon_aggregated_order`
--
ALTER TABLE `salesrule_coupon_aggregated_order`
  ADD PRIMARY KEY (`id`),
  ADD UNIQUE KEY `UNQ_1094D1FBBCBB11704A29DEF3ACC37D2B` (`period`,`store_id`,`order_status`,`coupon_code`),
  ADD KEY `SALESRULE_COUPON_AGGREGATED_ORDER_STORE_ID` (`store_id`),
  ADD KEY `SALESRULE_COUPON_AGGREGATED_ORDER_RULE_NAME` (`rule_name`);

--
-- Indexes for table `salesrule_coupon_aggregated_updated`
--
ALTER TABLE `salesrule_coupon_aggregated_updated`
  ADD PRIMARY KEY (`id`),
  ADD UNIQUE KEY `UNQ_7196FA120A4F0F84E1B66605E87E213E` (`period`,`store_id`,`order_status`,`coupon_code`),
  ADD KEY `SALESRULE_COUPON_AGGREGATED_UPDATED_STORE_ID` (`store_id`),
  ADD KEY `SALESRULE_COUPON_AGGREGATED_UPDATED_RULE_NAME` (`rule_name`);

--
-- Indexes for table `salesrule_coupon_usage`
--
ALTER TABLE `salesrule_coupon_usage`
  ADD PRIMARY KEY (`coupon_id`,`customer_id`),
  ADD KEY `SALESRULE_COUPON_USAGE_CUSTOMER_ID` (`customer_id`);

--
-- Indexes for table `salesrule_customer`
--
ALTER TABLE `salesrule_customer`
  ADD PRIMARY KEY (`rule_customer_id`),
  ADD KEY `SALESRULE_CUSTOMER_RULE_ID_CUSTOMER_ID` (`rule_id`,`customer_id`),
  ADD KEY `SALESRULE_CUSTOMER_CUSTOMER_ID_RULE_ID` (`customer_id`,`rule_id`);

--
-- Indexes for table `salesrule_customer_group`
--
ALTER TABLE `salesrule_customer_group`
  ADD PRIMARY KEY (`rule_id`,`customer_group_id`),
  ADD KEY `SALESRULE_CUSTOMER_GROUP_CUSTOMER_GROUP_ID` (`customer_group_id`);

--
-- Indexes for table `salesrule_label`
--
ALTER TABLE `salesrule_label`
  ADD PRIMARY KEY (`label_id`),
  ADD UNIQUE KEY `SALESRULE_LABEL_RULE_ID_STORE_ID` (`rule_id`,`store_id`),
  ADD KEY `SALESRULE_LABEL_STORE_ID` (`store_id`);

--
-- Indexes for table `salesrule_product_attribute`
--
ALTER TABLE `salesrule_product_attribute`
  ADD PRIMARY KEY (`rule_id`,`website_id`,`customer_group_id`,`attribute_id`),
  ADD KEY `SALESRULE_PRODUCT_ATTRIBUTE_WEBSITE_ID` (`website_id`),
  ADD KEY `SALESRULE_PRODUCT_ATTRIBUTE_CUSTOMER_GROUP_ID` (`customer_group_id`),
  ADD KEY `SALESRULE_PRODUCT_ATTRIBUTE_ATTRIBUTE_ID` (`attribute_id`);

--
-- Indexes for table `salesrule_website`
--
ALTER TABLE `salesrule_website`
  ADD PRIMARY KEY (`rule_id`,`website_id`),
  ADD KEY `SALESRULE_WEBSITE_WEBSITE_ID` (`website_id`);

--
-- Indexes for table `sales_bestsellers_aggregated_daily`
--
ALTER TABLE `sales_bestsellers_aggregated_daily`
  ADD PRIMARY KEY (`id`),
  ADD UNIQUE KEY `SALES_BESTSELLERS_AGGREGATED_DAILY_PERIOD_STORE_ID_PRODUCT_ID` (`period`,`store_id`,`product_id`),
  ADD KEY `SALES_BESTSELLERS_AGGREGATED_DAILY_STORE_ID` (`store_id`),
  ADD KEY `SALES_BESTSELLERS_AGGREGATED_DAILY_PRODUCT_ID` (`product_id`);

--
-- Indexes for table `sales_bestsellers_aggregated_monthly`
--
ALTER TABLE `sales_bestsellers_aggregated_monthly`
  ADD PRIMARY KEY (`id`),
  ADD UNIQUE KEY `SALES_BESTSELLERS_AGGREGATED_MONTHLY_PERIOD_STORE_ID_PRODUCT_ID` (`period`,`store_id`,`product_id`),
  ADD KEY `SALES_BESTSELLERS_AGGREGATED_MONTHLY_STORE_ID` (`store_id`),
  ADD KEY `SALES_BESTSELLERS_AGGREGATED_MONTHLY_PRODUCT_ID` (`product_id`);

--
-- Indexes for table `sales_bestsellers_aggregated_yearly`
--
ALTER TABLE `sales_bestsellers_aggregated_yearly`
  ADD PRIMARY KEY (`id`),
  ADD UNIQUE KEY `SALES_BESTSELLERS_AGGREGATED_YEARLY_PERIOD_STORE_ID_PRODUCT_ID` (`period`,`store_id`,`product_id`),
  ADD KEY `SALES_BESTSELLERS_AGGREGATED_YEARLY_STORE_ID` (`store_id`),
  ADD KEY `SALES_BESTSELLERS_AGGREGATED_YEARLY_PRODUCT_ID` (`product_id`);

--
-- Indexes for table `sales_creditmemo`
--
ALTER TABLE `sales_creditmemo`
  ADD PRIMARY KEY (`entity_id`),
  ADD UNIQUE KEY `SALES_CREDITMEMO_INCREMENT_ID_STORE_ID` (`increment_id`,`store_id`),
  ADD KEY `SALES_CREDITMEMO_STORE_ID` (`store_id`),
  ADD KEY `SALES_CREDITMEMO_ORDER_ID` (`order_id`),
  ADD KEY `SALES_CREDITMEMO_CREDITMEMO_STATUS` (`creditmemo_status`),
  ADD KEY `SALES_CREDITMEMO_STATE` (`state`),
  ADD KEY `SALES_CREDITMEMO_CREATED_AT` (`created_at`),
  ADD KEY `SALES_CREDITMEMO_UPDATED_AT` (`updated_at`),
  ADD KEY `SALES_CREDITMEMO_SEND_EMAIL` (`send_email`),
  ADD KEY `SALES_CREDITMEMO_EMAIL_SENT` (`email_sent`);

--
-- Indexes for table `sales_creditmemo_comment`
--
ALTER TABLE `sales_creditmemo_comment`
  ADD PRIMARY KEY (`entity_id`),
  ADD KEY `SALES_CREDITMEMO_COMMENT_CREATED_AT` (`created_at`),
  ADD KEY `SALES_CREDITMEMO_COMMENT_PARENT_ID` (`parent_id`);

--
-- Indexes for table `sales_creditmemo_grid`
--
ALTER TABLE `sales_creditmemo_grid`
  ADD PRIMARY KEY (`entity_id`),
  ADD UNIQUE KEY `SALES_CREDITMEMO_GRID_INCREMENT_ID_STORE_ID` (`increment_id`,`store_id`),
  ADD KEY `SALES_CREDITMEMO_GRID_ORDER_INCREMENT_ID` (`order_increment_id`),
  ADD KEY `SALES_CREDITMEMO_GRID_CREATED_AT` (`created_at`),
  ADD KEY `SALES_CREDITMEMO_GRID_UPDATED_AT` (`updated_at`),
  ADD KEY `SALES_CREDITMEMO_GRID_ORDER_CREATED_AT` (`order_created_at`),
  ADD KEY `SALES_CREDITMEMO_GRID_STATE` (`state`),
  ADD KEY `SALES_CREDITMEMO_GRID_BILLING_NAME` (`billing_name`),
  ADD KEY `SALES_CREDITMEMO_GRID_ORDER_STATUS` (`order_status`),
  ADD KEY `SALES_CREDITMEMO_GRID_BASE_GRAND_TOTAL` (`base_grand_total`),
  ADD KEY `SALES_CREDITMEMO_GRID_STORE_ID` (`store_id`),
  ADD KEY `SALES_CREDITMEMO_GRID_ORDER_BASE_GRAND_TOTAL` (`order_base_grand_total`),
  ADD KEY `SALES_CREDITMEMO_GRID_ORDER_ID` (`order_id`);
ALTER TABLE `sales_creditmemo_grid` ADD FULLTEXT KEY `FTI_32B7BA885941A8254EE84AE650ABDC86` (`increment_id`,`order_increment_id`,`billing_name`,`billing_address`,`shipping_address`,`customer_name`,`customer_email`);

--
-- Indexes for table `sales_creditmemo_item`
--
ALTER TABLE `sales_creditmemo_item`
  ADD PRIMARY KEY (`entity_id`),
  ADD KEY `SALES_CREDITMEMO_ITEM_PARENT_ID` (`parent_id`);

--
-- Indexes for table `sales_invoice`
--
ALTER TABLE `sales_invoice`
  ADD PRIMARY KEY (`entity_id`),
  ADD UNIQUE KEY `SALES_INVOICE_INCREMENT_ID_STORE_ID` (`increment_id`,`store_id`),
  ADD KEY `SALES_INVOICE_STORE_ID` (`store_id`),
  ADD KEY `SALES_INVOICE_GRAND_TOTAL` (`grand_total`),
  ADD KEY `SALES_INVOICE_ORDER_ID` (`order_id`),
  ADD KEY `SALES_INVOICE_STATE` (`state`),
  ADD KEY `SALES_INVOICE_CREATED_AT` (`created_at`),
  ADD KEY `SALES_INVOICE_UPDATED_AT` (`updated_at`),
  ADD KEY `SALES_INVOICE_SEND_EMAIL` (`send_email`),
  ADD KEY `SALES_INVOICE_EMAIL_SENT` (`email_sent`);

--
-- Indexes for table `sales_invoiced_aggregated`
--
ALTER TABLE `sales_invoiced_aggregated`
  ADD PRIMARY KEY (`id`),
  ADD UNIQUE KEY `SALES_INVOICED_AGGREGATED_PERIOD_STORE_ID_ORDER_STATUS` (`period`,`store_id`,`order_status`),
  ADD KEY `SALES_INVOICED_AGGREGATED_STORE_ID` (`store_id`);

--
-- Indexes for table `sales_invoiced_aggregated_order`
--
ALTER TABLE `sales_invoiced_aggregated_order`
  ADD PRIMARY KEY (`id`),
  ADD UNIQUE KEY `SALES_INVOICED_AGGREGATED_ORDER_PERIOD_STORE_ID_ORDER_STATUS` (`period`,`store_id`,`order_status`),
  ADD KEY `SALES_INVOICED_AGGREGATED_ORDER_STORE_ID` (`store_id`);

--
-- Indexes for table `sales_invoice_comment`
--
ALTER TABLE `sales_invoice_comment`
  ADD PRIMARY KEY (`entity_id`),
  ADD KEY `SALES_INVOICE_COMMENT_CREATED_AT` (`created_at`),
  ADD KEY `SALES_INVOICE_COMMENT_PARENT_ID` (`parent_id`);

--
-- Indexes for table `sales_invoice_grid`
--
ALTER TABLE `sales_invoice_grid`
  ADD PRIMARY KEY (`entity_id`),
  ADD UNIQUE KEY `SALES_INVOICE_GRID_INCREMENT_ID_STORE_ID` (`increment_id`,`store_id`),
  ADD KEY `SALES_INVOICE_GRID_STORE_ID` (`store_id`),
  ADD KEY `SALES_INVOICE_GRID_GRAND_TOTAL` (`grand_total`),
  ADD KEY `SALES_INVOICE_GRID_ORDER_ID` (`order_id`),
  ADD KEY `SALES_INVOICE_GRID_STATE` (`state`),
  ADD KEY `SALES_INVOICE_GRID_ORDER_INCREMENT_ID` (`order_increment_id`),
  ADD KEY `SALES_INVOICE_GRID_CREATED_AT` (`created_at`),
  ADD KEY `SALES_INVOICE_GRID_UPDATED_AT` (`updated_at`),
  ADD KEY `SALES_INVOICE_GRID_ORDER_CREATED_AT` (`order_created_at`),
  ADD KEY `SALES_INVOICE_GRID_BILLING_NAME` (`billing_name`);
ALTER TABLE `sales_invoice_grid` ADD FULLTEXT KEY `FTI_95D9C924DD6A8734EB8B5D01D60F90DE` (`increment_id`,`order_increment_id`,`billing_name`,`billing_address`,`shipping_address`,`customer_name`,`customer_email`);

--
-- Indexes for table `sales_invoice_item`
--
ALTER TABLE `sales_invoice_item`
  ADD PRIMARY KEY (`entity_id`),
  ADD KEY `SALES_INVOICE_ITEM_PARENT_ID` (`parent_id`);

--
-- Indexes for table `sales_order`
--
ALTER TABLE `sales_order`
  ADD PRIMARY KEY (`entity_id`),
  ADD UNIQUE KEY `SALES_ORDER_INCREMENT_ID_STORE_ID` (`increment_id`,`store_id`),
  ADD KEY `SALES_ORDER_STATUS` (`status`),
  ADD KEY `SALES_ORDER_STATE` (`state`),
  ADD KEY `SALES_ORDER_STORE_ID` (`store_id`),
  ADD KEY `SALES_ORDER_CREATED_AT` (`created_at`),
  ADD KEY `SALES_ORDER_CUSTOMER_ID` (`customer_id`),
  ADD KEY `SALES_ORDER_EXT_ORDER_ID` (`ext_order_id`),
  ADD KEY `SALES_ORDER_QUOTE_ID` (`quote_id`),
  ADD KEY `SALES_ORDER_UPDATED_AT` (`updated_at`),
  ADD KEY `SALES_ORDER_SEND_EMAIL` (`send_email`),
  ADD KEY `SALES_ORDER_EMAIL_SENT` (`email_sent`);

--
-- Indexes for table `sales_order_address`
--
ALTER TABLE `sales_order_address`
  ADD PRIMARY KEY (`entity_id`),
  ADD KEY `SALES_ORDER_ADDRESS_PARENT_ID` (`parent_id`);

--
-- Indexes for table `sales_order_aggregated_created`
--
ALTER TABLE `sales_order_aggregated_created`
  ADD PRIMARY KEY (`id`),
  ADD UNIQUE KEY `SALES_ORDER_AGGREGATED_CREATED_PERIOD_STORE_ID_ORDER_STATUS` (`period`,`store_id`,`order_status`),
  ADD KEY `SALES_ORDER_AGGREGATED_CREATED_STORE_ID` (`store_id`);

--
-- Indexes for table `sales_order_aggregated_updated`
--
ALTER TABLE `sales_order_aggregated_updated`
  ADD PRIMARY KEY (`id`),
  ADD UNIQUE KEY `SALES_ORDER_AGGREGATED_UPDATED_PERIOD_STORE_ID_ORDER_STATUS` (`period`,`store_id`,`order_status`),
  ADD KEY `SALES_ORDER_AGGREGATED_UPDATED_STORE_ID` (`store_id`);

--
-- Indexes for table `sales_order_grid`
--
ALTER TABLE `sales_order_grid`
  ADD PRIMARY KEY (`entity_id`),
  ADD UNIQUE KEY `SALES_ORDER_GRID_INCREMENT_ID_STORE_ID` (`increment_id`,`store_id`),
  ADD KEY `SALES_ORDER_GRID_STATUS` (`status`),
  ADD KEY `SALES_ORDER_GRID_STORE_ID` (`store_id`),
  ADD KEY `SALES_ORDER_GRID_BASE_GRAND_TOTAL` (`base_grand_total`),
  ADD KEY `SALES_ORDER_GRID_BASE_TOTAL_PAID` (`base_total_paid`),
  ADD KEY `SALES_ORDER_GRID_GRAND_TOTAL` (`grand_total`),
  ADD KEY `SALES_ORDER_GRID_TOTAL_PAID` (`total_paid`),
  ADD KEY `SALES_ORDER_GRID_SHIPPING_NAME` (`shipping_name`),
  ADD KEY `SALES_ORDER_GRID_BILLING_NAME` (`billing_name`),
  ADD KEY `SALES_ORDER_GRID_CREATED_AT` (`created_at`),
  ADD KEY `SALES_ORDER_GRID_CUSTOMER_ID` (`customer_id`),
  ADD KEY `SALES_ORDER_GRID_UPDATED_AT` (`updated_at`);
ALTER TABLE `sales_order_grid` ADD FULLTEXT KEY `FTI_65B9E9925EC58F0C7C2E2F6379C233E7` (`increment_id`,`billing_name`,`shipping_name`,`shipping_address`,`billing_address`,`customer_name`,`customer_email`);

--
-- Indexes for table `sales_order_item`
--
ALTER TABLE `sales_order_item`
  ADD PRIMARY KEY (`item_id`),
  ADD KEY `SALES_ORDER_ITEM_ORDER_ID` (`order_id`),
  ADD KEY `SALES_ORDER_ITEM_STORE_ID` (`store_id`);

--
-- Indexes for table `sales_order_payment`
--
ALTER TABLE `sales_order_payment`
  ADD PRIMARY KEY (`entity_id`),
  ADD KEY `SALES_ORDER_PAYMENT_PARENT_ID` (`parent_id`);

--
-- Indexes for table `sales_order_status`
--
ALTER TABLE `sales_order_status`
  ADD PRIMARY KEY (`status`);

--
-- Indexes for table `sales_order_status_history`
--
ALTER TABLE `sales_order_status_history`
  ADD PRIMARY KEY (`entity_id`),
  ADD KEY `SALES_ORDER_STATUS_HISTORY_PARENT_ID` (`parent_id`),
  ADD KEY `SALES_ORDER_STATUS_HISTORY_CREATED_AT` (`created_at`);

--
-- Indexes for table `sales_order_status_label`
--
ALTER TABLE `sales_order_status_label`
  ADD PRIMARY KEY (`status`,`store_id`),
  ADD KEY `SALES_ORDER_STATUS_LABEL_STORE_ID` (`store_id`);

--
-- Indexes for table `sales_order_status_state`
--
ALTER TABLE `sales_order_status_state`
  ADD PRIMARY KEY (`status`,`state`);

--
-- Indexes for table `sales_order_tax`
--
ALTER TABLE `sales_order_tax`
  ADD PRIMARY KEY (`tax_id`),
  ADD KEY `SALES_ORDER_TAX_ORDER_ID_PRIORITY_POSITION` (`order_id`,`priority`,`position`);

--
-- Indexes for table `sales_order_tax_item`
--
ALTER TABLE `sales_order_tax_item`
  ADD PRIMARY KEY (`tax_item_id`),
  ADD UNIQUE KEY `SALES_ORDER_TAX_ITEM_TAX_ID_ITEM_ID` (`tax_id`,`item_id`),
  ADD KEY `SALES_ORDER_TAX_ITEM_ITEM_ID` (`item_id`),
  ADD KEY `SALES_ORDER_TAX_ITEM_ASSOCIATED_ITEM_ID_SALES_ORDER_ITEM_ITEM_ID` (`associated_item_id`);

--
-- Indexes for table `sales_payment_transaction`
--
ALTER TABLE `sales_payment_transaction`
  ADD PRIMARY KEY (`transaction_id`),
  ADD UNIQUE KEY `SALES_PAYMENT_TRANSACTION_ORDER_ID_PAYMENT_ID_TXN_ID` (`order_id`,`payment_id`,`txn_id`),
  ADD KEY `SALES_PAYMENT_TRANSACTION_PARENT_ID` (`parent_id`),
  ADD KEY `SALES_PAYMENT_TRANSACTION_PAYMENT_ID` (`payment_id`);

--
-- Indexes for table `sales_refunded_aggregated`
--
ALTER TABLE `sales_refunded_aggregated`
  ADD PRIMARY KEY (`id`),
  ADD UNIQUE KEY `SALES_REFUNDED_AGGREGATED_PERIOD_STORE_ID_ORDER_STATUS` (`period`,`store_id`,`order_status`),
  ADD KEY `SALES_REFUNDED_AGGREGATED_STORE_ID` (`store_id`);

--
-- Indexes for table `sales_refunded_aggregated_order`
--
ALTER TABLE `sales_refunded_aggregated_order`
  ADD PRIMARY KEY (`id`),
  ADD UNIQUE KEY `SALES_REFUNDED_AGGREGATED_ORDER_PERIOD_STORE_ID_ORDER_STATUS` (`period`,`store_id`,`order_status`),
  ADD KEY `SALES_REFUNDED_AGGREGATED_ORDER_STORE_ID` (`store_id`);

--
-- Indexes for table `sales_sequence_meta`
--
ALTER TABLE `sales_sequence_meta`
  ADD PRIMARY KEY (`meta_id`),
  ADD UNIQUE KEY `SALES_SEQUENCE_META_ENTITY_TYPE_STORE_ID` (`entity_type`,`store_id`);

--
-- Indexes for table `sales_sequence_profile`
--
ALTER TABLE `sales_sequence_profile`
  ADD PRIMARY KEY (`profile_id`),
  ADD UNIQUE KEY `SALES_SEQUENCE_PROFILE_META_ID_PREFIX_SUFFIX` (`meta_id`,`prefix`,`suffix`);

--
-- Indexes for table `sales_shipment`
--
ALTER TABLE `sales_shipment`
  ADD PRIMARY KEY (`entity_id`),
  ADD UNIQUE KEY `SALES_SHIPMENT_INCREMENT_ID_STORE_ID` (`increment_id`,`store_id`),
  ADD KEY `SALES_SHIPMENT_STORE_ID` (`store_id`),
  ADD KEY `SALES_SHIPMENT_TOTAL_QTY` (`total_qty`),
  ADD KEY `SALES_SHIPMENT_ORDER_ID` (`order_id`),
  ADD KEY `SALES_SHIPMENT_CREATED_AT` (`created_at`),
  ADD KEY `SALES_SHIPMENT_UPDATED_AT` (`updated_at`),
  ADD KEY `SALES_SHIPMENT_SEND_EMAIL` (`send_email`),
  ADD KEY `SALES_SHIPMENT_EMAIL_SENT` (`email_sent`);

--
-- Indexes for table `sales_shipment_comment`
--
ALTER TABLE `sales_shipment_comment`
  ADD PRIMARY KEY (`entity_id`),
  ADD KEY `SALES_SHIPMENT_COMMENT_CREATED_AT` (`created_at`),
  ADD KEY `SALES_SHIPMENT_COMMENT_PARENT_ID` (`parent_id`);

--
-- Indexes for table `sales_shipment_grid`
--
ALTER TABLE `sales_shipment_grid`
  ADD PRIMARY KEY (`entity_id`),
  ADD UNIQUE KEY `SALES_SHIPMENT_GRID_INCREMENT_ID_STORE_ID` (`increment_id`,`store_id`),
  ADD KEY `SALES_SHIPMENT_GRID_STORE_ID` (`store_id`),
  ADD KEY `SALES_SHIPMENT_GRID_TOTAL_QTY` (`total_qty`),
  ADD KEY `SALES_SHIPMENT_GRID_ORDER_INCREMENT_ID` (`order_increment_id`),
  ADD KEY `SALES_SHIPMENT_GRID_SHIPMENT_STATUS` (`shipment_status`),
  ADD KEY `SALES_SHIPMENT_GRID_ORDER_STATUS` (`order_status`),
  ADD KEY `SALES_SHIPMENT_GRID_CREATED_AT` (`created_at`),
  ADD KEY `SALES_SHIPMENT_GRID_UPDATED_AT` (`updated_at`),
  ADD KEY `SALES_SHIPMENT_GRID_ORDER_CREATED_AT` (`order_created_at`),
  ADD KEY `SALES_SHIPMENT_GRID_SHIPPING_NAME` (`shipping_name`),
  ADD KEY `SALES_SHIPMENT_GRID_BILLING_NAME` (`billing_name`);
ALTER TABLE `sales_shipment_grid` ADD FULLTEXT KEY `FTI_086B40C8955F167B8EA76653437879B4` (`increment_id`,`order_increment_id`,`shipping_name`,`customer_name`,`customer_email`,`billing_address`,`shipping_address`);

--
-- Indexes for table `sales_shipment_item`
--
ALTER TABLE `sales_shipment_item`
  ADD PRIMARY KEY (`entity_id`),
  ADD KEY `SALES_SHIPMENT_ITEM_PARENT_ID` (`parent_id`);

--
-- Indexes for table `sales_shipment_track`
--
ALTER TABLE `sales_shipment_track`
  ADD PRIMARY KEY (`entity_id`),
  ADD KEY `SALES_SHIPMENT_TRACK_PARENT_ID` (`parent_id`),
  ADD KEY `SALES_SHIPMENT_TRACK_ORDER_ID` (`order_id`),
  ADD KEY `SALES_SHIPMENT_TRACK_CREATED_AT` (`created_at`);

--
-- Indexes for table `sales_shipping_aggregated`
--
ALTER TABLE `sales_shipping_aggregated`
  ADD PRIMARY KEY (`id`),
  ADD UNIQUE KEY `SALES_SHPP_AGGRED_PERIOD_STORE_ID_ORDER_STS_SHPP_DESCRIPTION` (`period`,`store_id`,`order_status`,`shipping_description`),
  ADD KEY `SALES_SHIPPING_AGGREGATED_STORE_ID` (`store_id`);

--
-- Indexes for table `sales_shipping_aggregated_order`
--
ALTER TABLE `sales_shipping_aggregated_order`
  ADD PRIMARY KEY (`id`),
  ADD UNIQUE KEY `UNQ_C05FAE47282EEA68654D0924E946761F` (`period`,`store_id`,`order_status`,`shipping_description`),
  ADD KEY `SALES_SHIPPING_AGGREGATED_ORDER_STORE_ID` (`store_id`);

--
-- Indexes for table `search_query`
--
ALTER TABLE `search_query`
  ADD PRIMARY KEY (`query_id`),
  ADD UNIQUE KEY `SEARCH_QUERY_QUERY_TEXT_STORE_ID` (`query_text`,`store_id`),
  ADD KEY `SEARCH_QUERY_QUERY_TEXT_STORE_ID_POPULARITY` (`query_text`,`store_id`,`popularity`),
  ADD KEY `SEARCH_QUERY_STORE_ID` (`store_id`),
  ADD KEY `SEARCH_QUERY_IS_PROCESSED` (`is_processed`),
  ADD KEY `SEARCH_QUERY_SYNONYM_FOR` (`synonym_for`);

--
-- Indexes for table `sendfriend_log`
--
ALTER TABLE `sendfriend_log`
  ADD PRIMARY KEY (`log_id`),
  ADD KEY `SENDFRIEND_LOG_IP` (`ip`),
  ADD KEY `SENDFRIEND_LOG_TIME` (`time`);

--
-- Indexes for table `sequence_creditmemo_0`
--
ALTER TABLE `sequence_creditmemo_0`
  ADD PRIMARY KEY (`sequence_value`);

--
-- Indexes for table `sequence_creditmemo_1`
--
ALTER TABLE `sequence_creditmemo_1`
  ADD PRIMARY KEY (`sequence_value`);

--
-- Indexes for table `sequence_creditmemo_2`
--
ALTER TABLE `sequence_creditmemo_2`
  ADD PRIMARY KEY (`sequence_value`);

--
-- Indexes for table `sequence_invoice_0`
--
ALTER TABLE `sequence_invoice_0`
  ADD PRIMARY KEY (`sequence_value`);

--
-- Indexes for table `sequence_invoice_1`
--
ALTER TABLE `sequence_invoice_1`
  ADD PRIMARY KEY (`sequence_value`);

--
-- Indexes for table `sequence_invoice_2`
--
ALTER TABLE `sequence_invoice_2`
  ADD PRIMARY KEY (`sequence_value`);

--
-- Indexes for table `sequence_order_0`
--
ALTER TABLE `sequence_order_0`
  ADD PRIMARY KEY (`sequence_value`);

--
-- Indexes for table `sequence_order_1`
--
ALTER TABLE `sequence_order_1`
  ADD PRIMARY KEY (`sequence_value`);

--
-- Indexes for table `sequence_order_2`
--
ALTER TABLE `sequence_order_2`
  ADD PRIMARY KEY (`sequence_value`);

--
-- Indexes for table `sequence_shipment_0`
--
ALTER TABLE `sequence_shipment_0`
  ADD PRIMARY KEY (`sequence_value`);

--
-- Indexes for table `sequence_shipment_1`
--
ALTER TABLE `sequence_shipment_1`
  ADD PRIMARY KEY (`sequence_value`);

--
-- Indexes for table `sequence_shipment_2`
--
ALTER TABLE `sequence_shipment_2`
  ADD PRIMARY KEY (`sequence_value`);

--
-- Indexes for table `session`
--
ALTER TABLE `session`
  ADD PRIMARY KEY (`session_id`);

--
-- Indexes for table `setup_module`
--
ALTER TABLE `setup_module`
  ADD PRIMARY KEY (`module`);

--
-- Indexes for table `shipping_tablerate`
--
ALTER TABLE `shipping_tablerate`
  ADD PRIMARY KEY (`pk`),
  ADD UNIQUE KEY `UNQ_D60821CDB2AFACEE1566CFC02D0D4CAA` (`website_id`,`dest_country_id`,`dest_region_id`,`dest_zip`,`condition_name`,`condition_value`);

--
-- Indexes for table `sitemap`
--
ALTER TABLE `sitemap`
  ADD PRIMARY KEY (`sitemap_id`),
  ADD KEY `SITEMAP_STORE_ID` (`store_id`);

--
-- Indexes for table `store`
--
ALTER TABLE `store`
  ADD PRIMARY KEY (`store_id`),
  ADD UNIQUE KEY `STORE_CODE` (`code`),
  ADD KEY `STORE_WEBSITE_ID` (`website_id`),
  ADD KEY `STORE_IS_ACTIVE_SORT_ORDER` (`is_active`,`sort_order`),
  ADD KEY `STORE_GROUP_ID` (`group_id`);

--
-- Indexes for table `store_group`
--
ALTER TABLE `store_group`
  ADD PRIMARY KEY (`group_id`),
  ADD KEY `STORE_GROUP_WEBSITE_ID` (`website_id`),
  ADD KEY `STORE_GROUP_DEFAULT_STORE_ID` (`default_store_id`);

--
-- Indexes for table `store_website`
--
ALTER TABLE `store_website`
  ADD PRIMARY KEY (`website_id`),
  ADD UNIQUE KEY `STORE_WEBSITE_CODE` (`code`),
  ADD KEY `STORE_WEBSITE_SORT_ORDER` (`sort_order`),
  ADD KEY `STORE_WEBSITE_DEFAULT_GROUP_ID` (`default_group_id`);

--
-- Indexes for table `tax_calculation`
--
ALTER TABLE `tax_calculation`
  ADD PRIMARY KEY (`tax_calculation_id`),
  ADD KEY `TAX_CALCULATION_TAX_CALCULATION_RULE_ID` (`tax_calculation_rule_id`),
  ADD KEY `TAX_CALCULATION_CUSTOMER_TAX_CLASS_ID` (`customer_tax_class_id`),
  ADD KEY `TAX_CALCULATION_PRODUCT_TAX_CLASS_ID` (`product_tax_class_id`),
  ADD KEY `TAX_CALC_TAX_CALC_RATE_ID_CSTR_TAX_CLASS_ID_PRD_TAX_CLASS_ID` (`tax_calculation_rate_id`,`customer_tax_class_id`,`product_tax_class_id`);

--
-- Indexes for table `tax_calculation_rate`
--
ALTER TABLE `tax_calculation_rate`
  ADD PRIMARY KEY (`tax_calculation_rate_id`),
  ADD KEY `TAX_CALCULATION_RATE_TAX_COUNTRY_ID_TAX_REGION_ID_TAX_POSTCODE` (`tax_country_id`,`tax_region_id`,`tax_postcode`),
  ADD KEY `TAX_CALCULATION_RATE_CODE` (`code`),
  ADD KEY `IDX_CA799F1E2CB843495F601E56C84A626D` (`tax_calculation_rate_id`,`tax_country_id`,`tax_region_id`,`zip_is_range`,`tax_postcode`);

--
-- Indexes for table `tax_calculation_rate_title`
--
ALTER TABLE `tax_calculation_rate_title`
  ADD PRIMARY KEY (`tax_calculation_rate_title_id`),
  ADD KEY `TAX_CALCULATION_RATE_TITLE_TAX_CALCULATION_RATE_ID_STORE_ID` (`tax_calculation_rate_id`,`store_id`),
  ADD KEY `TAX_CALCULATION_RATE_TITLE_STORE_ID` (`store_id`);

--
-- Indexes for table `tax_calculation_rule`
--
ALTER TABLE `tax_calculation_rule`
  ADD PRIMARY KEY (`tax_calculation_rule_id`),
  ADD KEY `TAX_CALCULATION_RULE_PRIORITY_POSITION` (`priority`,`position`),
  ADD KEY `TAX_CALCULATION_RULE_CODE` (`code`);

--
-- Indexes for table `tax_class`
--
ALTER TABLE `tax_class`
  ADD PRIMARY KEY (`class_id`);

--
-- Indexes for table `tax_order_aggregated_created`
--
ALTER TABLE `tax_order_aggregated_created`
  ADD PRIMARY KEY (`id`),
  ADD UNIQUE KEY `TAX_ORDER_AGGRED_CREATED_PERIOD_STORE_ID_CODE_PERCENT_ORDER_STS` (`period`,`store_id`,`code`,`percent`,`order_status`),
  ADD KEY `TAX_ORDER_AGGREGATED_CREATED_STORE_ID` (`store_id`);

--
-- Indexes for table `tax_order_aggregated_updated`
--
ALTER TABLE `tax_order_aggregated_updated`
  ADD PRIMARY KEY (`id`),
  ADD UNIQUE KEY `TAX_ORDER_AGGRED_UPDATED_PERIOD_STORE_ID_CODE_PERCENT_ORDER_STS` (`period`,`store_id`,`code`,`percent`,`order_status`),
  ADD KEY `TAX_ORDER_AGGREGATED_UPDATED_STORE_ID` (`store_id`);

--
-- Indexes for table `theme`
--
ALTER TABLE `theme`
  ADD PRIMARY KEY (`theme_id`);

--
-- Indexes for table `theme_file`
--
ALTER TABLE `theme_file`
  ADD PRIMARY KEY (`theme_files_id`),
  ADD KEY `THEME_FILE_THEME_ID_THEME_THEME_ID` (`theme_id`);

--
-- Indexes for table `translation`
--
ALTER TABLE `translation`
  ADD PRIMARY KEY (`key_id`),
  ADD UNIQUE KEY `TRANSLATION_STORE_ID_LOCALE_CRC_STRING_STRING` (`store_id`,`locale`,`crc_string`,`string`);

--
-- Indexes for table `ui_bookmark`
--
ALTER TABLE `ui_bookmark`
  ADD PRIMARY KEY (`bookmark_id`),
  ADD KEY `UI_BOOKMARK_USER_ID_NAMESPACE_IDENTIFIER` (`user_id`,`namespace`,`identifier`);

--
-- Indexes for table `url_rewrite`
--
ALTER TABLE `url_rewrite`
  ADD PRIMARY KEY (`url_rewrite_id`),
  ADD UNIQUE KEY `URL_REWRITE_REQUEST_PATH_STORE_ID` (`request_path`,`store_id`),
  ADD KEY `URL_REWRITE_TARGET_PATH` (`target_path`),
  ADD KEY `URL_REWRITE_STORE_ID_ENTITY_ID` (`store_id`,`entity_id`);

--
-- Indexes for table `variable`
--
ALTER TABLE `variable`
  ADD PRIMARY KEY (`variable_id`),
  ADD UNIQUE KEY `VARIABLE_CODE` (`code`);

--
-- Indexes for table `variable_value`
--
ALTER TABLE `variable_value`
  ADD PRIMARY KEY (`value_id`),
  ADD UNIQUE KEY `VARIABLE_VALUE_VARIABLE_ID_STORE_ID` (`variable_id`,`store_id`),
  ADD KEY `VARIABLE_VALUE_STORE_ID` (`store_id`);

--
-- Indexes for table `weee_tax`
--
ALTER TABLE `weee_tax`
  ADD PRIMARY KEY (`value_id`),
  ADD KEY `WEEE_TAX_WEBSITE_ID` (`website_id`),
  ADD KEY `WEEE_TAX_ENTITY_ID` (`entity_id`),
  ADD KEY `WEEE_TAX_COUNTRY` (`country`),
  ADD KEY `WEEE_TAX_ATTRIBUTE_ID` (`attribute_id`);

--
-- Indexes for table `widget`
--
ALTER TABLE `widget`
  ADD PRIMARY KEY (`widget_id`),
  ADD KEY `WIDGET_WIDGET_CODE` (`widget_code`);

--
-- Indexes for table `widget_instance`
--
ALTER TABLE `widget_instance`
  ADD PRIMARY KEY (`instance_id`),
  ADD KEY `WIDGET_INSTANCE_THEME_ID_THEME_THEME_ID` (`theme_id`);

--
-- Indexes for table `widget_instance_page`
--
ALTER TABLE `widget_instance_page`
  ADD PRIMARY KEY (`page_id`),
  ADD KEY `WIDGET_INSTANCE_PAGE_INSTANCE_ID` (`instance_id`);

--
-- Indexes for table `widget_instance_page_layout`
--
ALTER TABLE `widget_instance_page_layout`
  ADD UNIQUE KEY `WIDGET_INSTANCE_PAGE_LAYOUT_LAYOUT_UPDATE_ID_PAGE_ID` (`layout_update_id`,`page_id`),
  ADD KEY `WIDGET_INSTANCE_PAGE_LAYOUT_PAGE_ID` (`page_id`);

--
-- Indexes for table `wishlist`
--
ALTER TABLE `wishlist`
  ADD PRIMARY KEY (`wishlist_id`),
  ADD UNIQUE KEY `WISHLIST_CUSTOMER_ID` (`customer_id`),
  ADD KEY `WISHLIST_SHARED` (`shared`);

--
-- Indexes for table `wishlist_item`
--
ALTER TABLE `wishlist_item`
  ADD PRIMARY KEY (`wishlist_item_id`),
  ADD KEY `WISHLIST_ITEM_WISHLIST_ID` (`wishlist_id`),
  ADD KEY `WISHLIST_ITEM_PRODUCT_ID` (`product_id`),
  ADD KEY `WISHLIST_ITEM_STORE_ID` (`store_id`);

--
-- Indexes for table `wishlist_item_option`
--
ALTER TABLE `wishlist_item_option`
  ADD PRIMARY KEY (`option_id`),
  ADD KEY `FK_A014B30B04B72DD0EAB3EECD779728D6` (`wishlist_item_id`);

--
-- AUTO_INCREMENT for dumped tables
--

--
-- AUTO_INCREMENT for table `adminnotification_inbox`
--
ALTER TABLE `adminnotification_inbox`
  MODIFY `notification_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Notification id';
--
-- AUTO_INCREMENT for table `admin_passwords`
--
ALTER TABLE `admin_passwords`
  MODIFY `password_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Password Id';
--
-- AUTO_INCREMENT for table `admin_user`
--
ALTER TABLE `admin_user`
  MODIFY `user_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'User ID', AUTO_INCREMENT=2;
--
-- AUTO_INCREMENT for table `authorization_role`
--
ALTER TABLE `authorization_role`
  MODIFY `role_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Role ID', AUTO_INCREMENT=3;
--
-- AUTO_INCREMENT for table `authorization_rule`
--
ALTER TABLE `authorization_rule`
  MODIFY `rule_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Rule ID', AUTO_INCREMENT=2;
--
-- AUTO_INCREMENT for table `cataloginventory_stock`
--
ALTER TABLE `cataloginventory_stock`
  MODIFY `stock_id` smallint(5) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Stock Id', AUTO_INCREMENT=2;
--
-- AUTO_INCREMENT for table `cataloginventory_stock_item`
--
ALTER TABLE `cataloginventory_stock_item`
  MODIFY `item_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Item Id', AUTO_INCREMENT=12;
--
-- AUTO_INCREMENT for table `catalogrule`
--
ALTER TABLE `catalogrule`
  MODIFY `rule_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Rule Id';
--
-- AUTO_INCREMENT for table `catalogrule_product`
--
ALTER TABLE `catalogrule_product`
  MODIFY `rule_product_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Rule Product Id';
--
-- AUTO_INCREMENT for table `catalogrule_product_price`
--
ALTER TABLE `catalogrule_product_price`
  MODIFY `rule_product_price_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Rule Product PriceId';
--
-- AUTO_INCREMENT for table `catalog_category_entity`
--
ALTER TABLE `catalog_category_entity`
  MODIFY `entity_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Entity ID', AUTO_INCREMENT=8;
--
-- AUTO_INCREMENT for table `catalog_category_entity_datetime`
--
ALTER TABLE `catalog_category_entity_datetime`
  MODIFY `value_id` int(11) NOT NULL AUTO_INCREMENT COMMENT 'Value ID', AUTO_INCREMENT=19;
--
-- AUTO_INCREMENT for table `catalog_category_entity_decimal`
--
ALTER TABLE `catalog_category_entity_decimal`
  MODIFY `value_id` int(11) NOT NULL AUTO_INCREMENT COMMENT 'Value ID', AUTO_INCREMENT=6;
--
-- AUTO_INCREMENT for table `catalog_category_entity_int`
--
ALTER TABLE `catalog_category_entity_int`
  MODIFY `value_id` int(11) NOT NULL AUTO_INCREMENT COMMENT 'Value ID', AUTO_INCREMENT=36;
--
-- AUTO_INCREMENT for table `catalog_category_entity_text`
--
ALTER TABLE `catalog_category_entity_text`
  MODIFY `value_id` int(11) NOT NULL AUTO_INCREMENT COMMENT 'Value ID', AUTO_INCREMENT=43;
--
-- AUTO_INCREMENT for table `catalog_category_entity_varchar`
--
ALTER TABLE `catalog_category_entity_varchar`
  MODIFY `value_id` int(11) NOT NULL AUTO_INCREMENT COMMENT 'Value ID', AUTO_INCREMENT=62;
--
-- AUTO_INCREMENT for table `catalog_compare_item`
--
ALTER TABLE `catalog_compare_item`
  MODIFY `catalog_compare_item_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Compare Item ID', AUTO_INCREMENT=12;
--
-- AUTO_INCREMENT for table `catalog_product_bundle_option`
--
ALTER TABLE `catalog_product_bundle_option`
  MODIFY `option_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Option Id', AUTO_INCREMENT=2;
--
-- AUTO_INCREMENT for table `catalog_product_bundle_option_value`
--
ALTER TABLE `catalog_product_bundle_option_value`
  MODIFY `value_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Value Id', AUTO_INCREMENT=4;
--
-- AUTO_INCREMENT for table `catalog_product_bundle_selection`
--
ALTER TABLE `catalog_product_bundle_selection`
  MODIFY `selection_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Selection Id', AUTO_INCREMENT=3;
--
-- AUTO_INCREMENT for table `catalog_product_entity`
--
ALTER TABLE `catalog_product_entity`
  MODIFY `entity_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Entity ID', AUTO_INCREMENT=13;
--
-- AUTO_INCREMENT for table `catalog_product_entity_datetime`
--
ALTER TABLE `catalog_product_entity_datetime`
  MODIFY `value_id` int(11) NOT NULL AUTO_INCREMENT COMMENT 'Value ID', AUTO_INCREMENT=123;
--
-- AUTO_INCREMENT for table `catalog_product_entity_decimal`
--
ALTER TABLE `catalog_product_entity_decimal`
  MODIFY `value_id` int(11) NOT NULL AUTO_INCREMENT COMMENT 'Value ID', AUTO_INCREMENT=70;
--
-- AUTO_INCREMENT for table `catalog_product_entity_gallery`
--
ALTER TABLE `catalog_product_entity_gallery`
  MODIFY `value_id` int(11) NOT NULL AUTO_INCREMENT COMMENT 'Value ID';
--
-- AUTO_INCREMENT for table `catalog_product_entity_int`
--
ALTER TABLE `catalog_product_entity_int`
  MODIFY `value_id` int(11) NOT NULL AUTO_INCREMENT COMMENT 'Value ID', AUTO_INCREMENT=74;
--
-- AUTO_INCREMENT for table `catalog_product_entity_media_gallery`
--
ALTER TABLE `catalog_product_entity_media_gallery`
  MODIFY `value_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Value ID', AUTO_INCREMENT=33;
--
-- AUTO_INCREMENT for table `catalog_product_entity_media_gallery_value`
--
ALTER TABLE `catalog_product_entity_media_gallery_value`
  MODIFY `record_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Record Id', AUTO_INCREMENT=109;
--
-- AUTO_INCREMENT for table `catalog_product_entity_text`
--
ALTER TABLE `catalog_product_entity_text`
  MODIFY `value_id` int(11) NOT NULL AUTO_INCREMENT COMMENT 'Value ID', AUTO_INCREMENT=66;
--
-- AUTO_INCREMENT for table `catalog_product_entity_tier_price`
--
ALTER TABLE `catalog_product_entity_tier_price`
  MODIFY `value_id` int(11) NOT NULL AUTO_INCREMENT COMMENT 'Value ID';
--
-- AUTO_INCREMENT for table `catalog_product_entity_varchar`
--
ALTER TABLE `catalog_product_entity_varchar`
  MODIFY `value_id` int(11) NOT NULL AUTO_INCREMENT COMMENT 'Value ID', AUTO_INCREMENT=246;
--
-- AUTO_INCREMENT for table `catalog_product_link`
--
ALTER TABLE `catalog_product_link`
  MODIFY `link_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Link ID', AUTO_INCREMENT=9;
--
-- AUTO_INCREMENT for table `catalog_product_link_attribute`
--
ALTER TABLE `catalog_product_link_attribute`
  MODIFY `product_link_attribute_id` smallint(5) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Product Link Attribute ID', AUTO_INCREMENT=6;
--
-- AUTO_INCREMENT for table `catalog_product_link_attribute_decimal`
--
ALTER TABLE `catalog_product_link_attribute_decimal`
  MODIFY `value_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Value ID', AUTO_INCREMENT=3;
--
-- AUTO_INCREMENT for table `catalog_product_link_attribute_int`
--
ALTER TABLE `catalog_product_link_attribute_int`
  MODIFY `value_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Value ID', AUTO_INCREMENT=9;
--
-- AUTO_INCREMENT for table `catalog_product_link_attribute_varchar`
--
ALTER TABLE `catalog_product_link_attribute_varchar`
  MODIFY `value_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Value ID';
--
-- AUTO_INCREMENT for table `catalog_product_link_type`
--
ALTER TABLE `catalog_product_link_type`
  MODIFY `link_type_id` smallint(5) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Link Type ID', AUTO_INCREMENT=6;
--
-- AUTO_INCREMENT for table `catalog_product_option`
--
ALTER TABLE `catalog_product_option`
  MODIFY `option_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Option ID';
--
-- AUTO_INCREMENT for table `catalog_product_option_price`
--
ALTER TABLE `catalog_product_option_price`
  MODIFY `option_price_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Option Price ID';
--
-- AUTO_INCREMENT for table `catalog_product_option_title`
--
ALTER TABLE `catalog_product_option_title`
  MODIFY `option_title_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Option Title ID';
--
-- AUTO_INCREMENT for table `catalog_product_option_type_price`
--
ALTER TABLE `catalog_product_option_type_price`
  MODIFY `option_type_price_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Option Type Price ID';
--
-- AUTO_INCREMENT for table `catalog_product_option_type_title`
--
ALTER TABLE `catalog_product_option_type_title`
  MODIFY `option_type_title_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Option Type Title ID';
--
-- AUTO_INCREMENT for table `catalog_product_option_type_value`
--
ALTER TABLE `catalog_product_option_type_value`
  MODIFY `option_type_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Option Type ID';
--
-- AUTO_INCREMENT for table `catalog_product_super_attribute`
--
ALTER TABLE `catalog_product_super_attribute`
  MODIFY `product_super_attribute_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Product Super Attribute ID', AUTO_INCREMENT=2;
--
-- AUTO_INCREMENT for table `catalog_product_super_attribute_label`
--
ALTER TABLE `catalog_product_super_attribute_label`
  MODIFY `value_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Value ID', AUTO_INCREMENT=3;
--
-- AUTO_INCREMENT for table `catalog_product_super_link`
--
ALTER TABLE `catalog_product_super_link`
  MODIFY `link_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Link ID', AUTO_INCREMENT=4;
--
-- AUTO_INCREMENT for table `checkout_agreement`
--
ALTER TABLE `checkout_agreement`
  MODIFY `agreement_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Agreement Id';
--
-- AUTO_INCREMENT for table `cms_block`
--
ALTER TABLE `cms_block`
  MODIFY `block_id` smallint(6) NOT NULL AUTO_INCREMENT COMMENT 'Block ID', AUTO_INCREMENT=15;
--
-- AUTO_INCREMENT for table `cms_page`
--
ALTER TABLE `cms_page`
  MODIFY `page_id` smallint(6) NOT NULL AUTO_INCREMENT COMMENT 'Page ID', AUTO_INCREMENT=6;
--
-- AUTO_INCREMENT for table `core_config_data`
--
ALTER TABLE `core_config_data`
  MODIFY `config_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Config Id', AUTO_INCREMENT=68;
--
-- AUTO_INCREMENT for table `cron_schedule`
--
ALTER TABLE `cron_schedule`
  MODIFY `schedule_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Schedule Id';
--
-- AUTO_INCREMENT for table `customer_address_entity`
--
ALTER TABLE `customer_address_entity`
  MODIFY `entity_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Entity Id', AUTO_INCREMENT=3;
--
-- AUTO_INCREMENT for table `customer_address_entity_datetime`
--
ALTER TABLE `customer_address_entity_datetime`
  MODIFY `value_id` int(11) NOT NULL AUTO_INCREMENT COMMENT 'Value Id';
--
-- AUTO_INCREMENT for table `customer_address_entity_decimal`
--
ALTER TABLE `customer_address_entity_decimal`
  MODIFY `value_id` int(11) NOT NULL AUTO_INCREMENT COMMENT 'Value Id';
--
-- AUTO_INCREMENT for table `customer_address_entity_int`
--
ALTER TABLE `customer_address_entity_int`
  MODIFY `value_id` int(11) NOT NULL AUTO_INCREMENT COMMENT 'Value Id';
--
-- AUTO_INCREMENT for table `customer_address_entity_text`
--
ALTER TABLE `customer_address_entity_text`
  MODIFY `value_id` int(11) NOT NULL AUTO_INCREMENT COMMENT 'Value Id';
--
-- AUTO_INCREMENT for table `customer_address_entity_varchar`
--
ALTER TABLE `customer_address_entity_varchar`
  MODIFY `value_id` int(11) NOT NULL AUTO_INCREMENT COMMENT 'Value Id';
--
-- AUTO_INCREMENT for table `customer_entity`
--
ALTER TABLE `customer_entity`
  MODIFY `entity_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Entity Id', AUTO_INCREMENT=3;
--
-- AUTO_INCREMENT for table `customer_entity_datetime`
--
ALTER TABLE `customer_entity_datetime`
  MODIFY `value_id` int(11) NOT NULL AUTO_INCREMENT COMMENT 'Value Id';
--
-- AUTO_INCREMENT for table `customer_entity_decimal`
--
ALTER TABLE `customer_entity_decimal`
  MODIFY `value_id` int(11) NOT NULL AUTO_INCREMENT COMMENT 'Value Id';
--
-- AUTO_INCREMENT for table `customer_entity_int`
--
ALTER TABLE `customer_entity_int`
  MODIFY `value_id` int(11) NOT NULL AUTO_INCREMENT COMMENT 'Value Id';
--
-- AUTO_INCREMENT for table `customer_entity_text`
--
ALTER TABLE `customer_entity_text`
  MODIFY `value_id` int(11) NOT NULL AUTO_INCREMENT COMMENT 'Value Id';
--
-- AUTO_INCREMENT for table `customer_entity_varchar`
--
ALTER TABLE `customer_entity_varchar`
  MODIFY `value_id` int(11) NOT NULL AUTO_INCREMENT COMMENT 'Value Id';
--
-- AUTO_INCREMENT for table `customer_group`
--
ALTER TABLE `customer_group`
  MODIFY `customer_group_id` smallint(5) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Customer Group Id', AUTO_INCREMENT=4;
--
-- AUTO_INCREMENT for table `customer_log`
--
ALTER TABLE `customer_log`
  MODIFY `log_id` int(11) NOT NULL AUTO_INCREMENT COMMENT 'Log ID', AUTO_INCREMENT=4;
--
-- AUTO_INCREMENT for table `customer_visitor`
--
ALTER TABLE `customer_visitor`
  MODIFY `visitor_id` bigint(20) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Visitor ID', AUTO_INCREMENT=162;
--
-- AUTO_INCREMENT for table `design_change`
--
ALTER TABLE `design_change`
  MODIFY `design_change_id` int(11) NOT NULL AUTO_INCREMENT COMMENT 'Design Change Id';
--
-- AUTO_INCREMENT for table `directory_country_format`
--
ALTER TABLE `directory_country_format`
  MODIFY `country_format_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Country Format Id';
--
-- AUTO_INCREMENT for table `directory_country_region`
--
ALTER TABLE `directory_country_region`
  MODIFY `region_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Region Id', AUTO_INCREMENT=512;
--
-- AUTO_INCREMENT for table `downloadable_link`
--
ALTER TABLE `downloadable_link`
  MODIFY `link_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Link ID';
--
-- AUTO_INCREMENT for table `downloadable_link_price`
--
ALTER TABLE `downloadable_link_price`
  MODIFY `price_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Price ID';
--
-- AUTO_INCREMENT for table `downloadable_link_purchased`
--
ALTER TABLE `downloadable_link_purchased`
  MODIFY `purchased_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Purchased ID';
--
-- AUTO_INCREMENT for table `downloadable_link_purchased_item`
--
ALTER TABLE `downloadable_link_purchased_item`
  MODIFY `item_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Item ID';
--
-- AUTO_INCREMENT for table `downloadable_link_title`
--
ALTER TABLE `downloadable_link_title`
  MODIFY `title_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Title ID';
--
-- AUTO_INCREMENT for table `downloadable_sample`
--
ALTER TABLE `downloadable_sample`
  MODIFY `sample_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Sample ID';
--
-- AUTO_INCREMENT for table `downloadable_sample_title`
--
ALTER TABLE `downloadable_sample_title`
  MODIFY `title_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Title ID';
--
-- AUTO_INCREMENT for table `eav_attribute`
--
ALTER TABLE `eav_attribute`
  MODIFY `attribute_id` smallint(5) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Attribute Id', AUTO_INCREMENT=131;
--
-- AUTO_INCREMENT for table `eav_attribute_group`
--
ALTER TABLE `eav_attribute_group`
  MODIFY `attribute_group_id` smallint(5) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Attribute Group Id', AUTO_INCREMENT=17;
--
-- AUTO_INCREMENT for table `eav_attribute_label`
--
ALTER TABLE `eav_attribute_label`
  MODIFY `attribute_label_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Attribute Label Id';
--
-- AUTO_INCREMENT for table `eav_attribute_option`
--
ALTER TABLE `eav_attribute_option`
  MODIFY `option_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Option Id', AUTO_INCREMENT=7;
--
-- AUTO_INCREMENT for table `eav_attribute_option_swatch`
--
ALTER TABLE `eav_attribute_option_swatch`
  MODIFY `swatch_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Swatch ID';
--
-- AUTO_INCREMENT for table `eav_attribute_option_value`
--
ALTER TABLE `eav_attribute_option_value`
  MODIFY `value_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Value Id', AUTO_INCREMENT=7;
--
-- AUTO_INCREMENT for table `eav_attribute_set`
--
ALTER TABLE `eav_attribute_set`
  MODIFY `attribute_set_id` smallint(5) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Attribute Set Id', AUTO_INCREMENT=9;
--
-- AUTO_INCREMENT for table `eav_entity`
--
ALTER TABLE `eav_entity`
  MODIFY `entity_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Entity Id';
--
-- AUTO_INCREMENT for table `eav_entity_attribute`
--
ALTER TABLE `eav_entity_attribute`
  MODIFY `entity_attribute_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Entity Attribute Id', AUTO_INCREMENT=131;
--
-- AUTO_INCREMENT for table `eav_entity_datetime`
--
ALTER TABLE `eav_entity_datetime`
  MODIFY `value_id` int(11) NOT NULL AUTO_INCREMENT COMMENT 'Value Id';
--
-- AUTO_INCREMENT for table `eav_entity_decimal`
--
ALTER TABLE `eav_entity_decimal`
  MODIFY `value_id` int(11) NOT NULL AUTO_INCREMENT COMMENT 'Value Id';
--
-- AUTO_INCREMENT for table `eav_entity_int`
--
ALTER TABLE `eav_entity_int`
  MODIFY `value_id` int(11) NOT NULL AUTO_INCREMENT COMMENT 'Value Id';
--
-- AUTO_INCREMENT for table `eav_entity_store`
--
ALTER TABLE `eav_entity_store`
  MODIFY `entity_store_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Entity Store Id';
--
-- AUTO_INCREMENT for table `eav_entity_text`
--
ALTER TABLE `eav_entity_text`
  MODIFY `value_id` int(11) NOT NULL AUTO_INCREMENT COMMENT 'Value Id';
--
-- AUTO_INCREMENT for table `eav_entity_type`
--
ALTER TABLE `eav_entity_type`
  MODIFY `entity_type_id` smallint(5) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Entity Type Id', AUTO_INCREMENT=9;
--
-- AUTO_INCREMENT for table `eav_entity_varchar`
--
ALTER TABLE `eav_entity_varchar`
  MODIFY `value_id` int(11) NOT NULL AUTO_INCREMENT COMMENT 'Value Id';
--
-- AUTO_INCREMENT for table `eav_form_element`
--
ALTER TABLE `eav_form_element`
  MODIFY `element_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Element Id', AUTO_INCREMENT=43;
--
-- AUTO_INCREMENT for table `eav_form_fieldset`
--
ALTER TABLE `eav_form_fieldset`
  MODIFY `fieldset_id` smallint(5) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Fieldset Id';
--
-- AUTO_INCREMENT for table `eav_form_type`
--
ALTER TABLE `eav_form_type`
  MODIFY `type_id` smallint(5) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Type Id', AUTO_INCREMENT=5;
--
-- AUTO_INCREMENT for table `email_template`
--
ALTER TABLE `email_template`
  MODIFY `template_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Template ID';
--
-- AUTO_INCREMENT for table `flag`
--
ALTER TABLE `flag`
  MODIFY `flag_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Flag Id';
--
-- AUTO_INCREMENT for table `gift_message`
--
ALTER TABLE `gift_message`
  MODIFY `gift_message_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'GiftMessage Id';
--
-- AUTO_INCREMENT for table `googleoptimizer_code`
--
ALTER TABLE `googleoptimizer_code`
  MODIFY `code_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Google experiment code id';
--
-- AUTO_INCREMENT for table `importexport_importdata`
--
ALTER TABLE `importexport_importdata`
  MODIFY `id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Id';
--
-- AUTO_INCREMENT for table `import_history`
--
ALTER TABLE `import_history`
  MODIFY `history_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'History record Id';
--
-- AUTO_INCREMENT for table `indexer_state`
--
ALTER TABLE `indexer_state`
  MODIFY `state_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Indexer State Id', AUTO_INCREMENT=10;
--
-- AUTO_INCREMENT for table `integration`
--
ALTER TABLE `integration`
  MODIFY `integration_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Integration ID';
--
-- AUTO_INCREMENT for table `layout_link`
--
ALTER TABLE `layout_link`
  MODIFY `layout_link_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Link Id';
--
-- AUTO_INCREMENT for table `layout_update`
--
ALTER TABLE `layout_update`
  MODIFY `layout_update_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Layout Update Id';
--
-- AUTO_INCREMENT for table `mview_state`
--
ALTER TABLE `mview_state`
  MODIFY `state_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'View State Id';
--
-- AUTO_INCREMENT for table `newsletter_problem`
--
ALTER TABLE `newsletter_problem`
  MODIFY `problem_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Problem Id';
--
-- AUTO_INCREMENT for table `newsletter_queue`
--
ALTER TABLE `newsletter_queue`
  MODIFY `queue_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Queue Id';
--
-- AUTO_INCREMENT for table `newsletter_queue_link`
--
ALTER TABLE `newsletter_queue_link`
  MODIFY `queue_link_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Queue Link Id';
--
-- AUTO_INCREMENT for table `newsletter_subscriber`
--
ALTER TABLE `newsletter_subscriber`
  MODIFY `subscriber_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Subscriber Id';
--
-- AUTO_INCREMENT for table `newsletter_template`
--
ALTER TABLE `newsletter_template`
  MODIFY `template_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Template ID';
--
-- AUTO_INCREMENT for table `oauth_consumer`
--
ALTER TABLE `oauth_consumer`
  MODIFY `entity_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Entity Id';
--
-- AUTO_INCREMENT for table `oauth_token`
--
ALTER TABLE `oauth_token`
  MODIFY `entity_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Entity ID';
--
-- AUTO_INCREMENT for table `oauth_token_request_log`
--
ALTER TABLE `oauth_token_request_log`
  MODIFY `log_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Log Id';
--
-- AUTO_INCREMENT for table `paypal_billing_agreement`
--
ALTER TABLE `paypal_billing_agreement`
  MODIFY `agreement_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Agreement Id';
--
-- AUTO_INCREMENT for table `paypal_cert`
--
ALTER TABLE `paypal_cert`
  MODIFY `cert_id` smallint(5) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Cert Id';
--
-- AUTO_INCREMENT for table `paypal_payment_transaction`
--
ALTER TABLE `paypal_payment_transaction`
  MODIFY `transaction_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Entity Id';
--
-- AUTO_INCREMENT for table `paypal_settlement_report`
--
ALTER TABLE `paypal_settlement_report`
  MODIFY `report_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Report Id';
--
-- AUTO_INCREMENT for table `paypal_settlement_report_row`
--
ALTER TABLE `paypal_settlement_report_row`
  MODIFY `row_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Row Id';
--
-- AUTO_INCREMENT for table `persistent_session`
--
ALTER TABLE `persistent_session`
  MODIFY `persistent_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Session id';
--
-- AUTO_INCREMENT for table `product_alert_price`
--
ALTER TABLE `product_alert_price`
  MODIFY `alert_price_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Product alert price id';
--
-- AUTO_INCREMENT for table `product_alert_stock`
--
ALTER TABLE `product_alert_stock`
  MODIFY `alert_stock_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Product alert stock id';
--
-- AUTO_INCREMENT for table `quote`
--
ALTER TABLE `quote`
  MODIFY `entity_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Entity Id', AUTO_INCREMENT=14;
--
-- AUTO_INCREMENT for table `quote_address`
--
ALTER TABLE `quote_address`
  MODIFY `address_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Address Id', AUTO_INCREMENT=29;
--
-- AUTO_INCREMENT for table `quote_address_item`
--
ALTER TABLE `quote_address_item`
  MODIFY `address_item_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Address Item Id', AUTO_INCREMENT=8;
--
-- AUTO_INCREMENT for table `quote_id_mask`
--
ALTER TABLE `quote_id_mask`
  MODIFY `entity_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Entity Id', AUTO_INCREMENT=13;
--
-- AUTO_INCREMENT for table `quote_item`
--
ALTER TABLE `quote_item`
  MODIFY `item_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Item Id', AUTO_INCREMENT=35;
--
-- AUTO_INCREMENT for table `quote_item_option`
--
ALTER TABLE `quote_item_option`
  MODIFY `option_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Option Id', AUTO_INCREMENT=68;
--
-- AUTO_INCREMENT for table `quote_payment`
--
ALTER TABLE `quote_payment`
  MODIFY `payment_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Payment Id', AUTO_INCREMENT=5;
--
-- AUTO_INCREMENT for table `quote_shipping_rate`
--
ALTER TABLE `quote_shipping_rate`
  MODIFY `rate_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Rate Id', AUTO_INCREMENT=4;
--
-- AUTO_INCREMENT for table `rating`
--
ALTER TABLE `rating`
  MODIFY `rating_id` smallint(5) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Rating Id', AUTO_INCREMENT=4;
--
-- AUTO_INCREMENT for table `rating_entity`
--
ALTER TABLE `rating_entity`
  MODIFY `entity_id` smallint(5) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Entity Id', AUTO_INCREMENT=4;
--
-- AUTO_INCREMENT for table `rating_option`
--
ALTER TABLE `rating_option`
  MODIFY `option_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Rating Option Id', AUTO_INCREMENT=16;
--
-- AUTO_INCREMENT for table `rating_option_vote`
--
ALTER TABLE `rating_option_vote`
  MODIFY `vote_id` bigint(20) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Vote id', AUTO_INCREMENT=40;
--
-- AUTO_INCREMENT for table `rating_option_vote_aggregated`
--
ALTER TABLE `rating_option_vote_aggregated`
  MODIFY `primary_id` int(11) NOT NULL AUTO_INCREMENT COMMENT 'Vote aggregation id', AUTO_INCREMENT=82;
--
-- AUTO_INCREMENT for table `reporting_counts`
--
ALTER TABLE `reporting_counts`
  MODIFY `entity_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Entity Id';
--
-- AUTO_INCREMENT for table `reporting_module_status`
--
ALTER TABLE `reporting_module_status`
  MODIFY `entity_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Module Id';
--
-- AUTO_INCREMENT for table `reporting_orders`
--
ALTER TABLE `reporting_orders`
  MODIFY `entity_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Entity Id';
--
-- AUTO_INCREMENT for table `reporting_system_updates`
--
ALTER TABLE `reporting_system_updates`
  MODIFY `entity_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Entity Id';
--
-- AUTO_INCREMENT for table `reporting_users`
--
ALTER TABLE `reporting_users`
  MODIFY `entity_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Entity Id';
--
-- AUTO_INCREMENT for table `report_compared_product_index`
--
ALTER TABLE `report_compared_product_index`
  MODIFY `index_id` bigint(20) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Index Id', AUTO_INCREMENT=10;
--
-- AUTO_INCREMENT for table `report_event`
--
ALTER TABLE `report_event`
  MODIFY `event_id` bigint(20) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Event Id', AUTO_INCREMENT=271;
--
-- AUTO_INCREMENT for table `report_event_types`
--
ALTER TABLE `report_event_types`
  MODIFY `event_type_id` smallint(5) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Event Type Id', AUTO_INCREMENT=7;
--
-- AUTO_INCREMENT for table `report_viewed_product_aggregated_daily`
--
ALTER TABLE `report_viewed_product_aggregated_daily`
  MODIFY `id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Id';
--
-- AUTO_INCREMENT for table `report_viewed_product_aggregated_monthly`
--
ALTER TABLE `report_viewed_product_aggregated_monthly`
  MODIFY `id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Id';
--
-- AUTO_INCREMENT for table `report_viewed_product_aggregated_yearly`
--
ALTER TABLE `report_viewed_product_aggregated_yearly`
  MODIFY `id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Id';
--
-- AUTO_INCREMENT for table `report_viewed_product_index`
--
ALTER TABLE `report_viewed_product_index`
  MODIFY `index_id` bigint(20) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Index Id', AUTO_INCREMENT=203;
--
-- AUTO_INCREMENT for table `review`
--
ALTER TABLE `review`
  MODIFY `review_id` bigint(20) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Review id', AUTO_INCREMENT=14;
--
-- AUTO_INCREMENT for table `review_detail`
--
ALTER TABLE `review_detail`
  MODIFY `detail_id` bigint(20) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Review detail id', AUTO_INCREMENT=14;
--
-- AUTO_INCREMENT for table `review_entity`
--
ALTER TABLE `review_entity`
  MODIFY `entity_id` smallint(5) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Review entity id', AUTO_INCREMENT=4;
--
-- AUTO_INCREMENT for table `review_entity_summary`
--
ALTER TABLE `review_entity_summary`
  MODIFY `primary_id` bigint(20) NOT NULL AUTO_INCREMENT COMMENT 'Summary review entity id', AUTO_INCREMENT=22;
--
-- AUTO_INCREMENT for table `review_status`
--
ALTER TABLE `review_status`
  MODIFY `status_id` smallint(5) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Status id', AUTO_INCREMENT=4;
--
-- AUTO_INCREMENT for table `salesrule`
--
ALTER TABLE `salesrule`
  MODIFY `rule_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Rule Id';
--
-- AUTO_INCREMENT for table `salesrule_coupon`
--
ALTER TABLE `salesrule_coupon`
  MODIFY `coupon_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Coupon Id';
--
-- AUTO_INCREMENT for table `salesrule_coupon_aggregated`
--
ALTER TABLE `salesrule_coupon_aggregated`
  MODIFY `id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Id';
--
-- AUTO_INCREMENT for table `salesrule_coupon_aggregated_order`
--
ALTER TABLE `salesrule_coupon_aggregated_order`
  MODIFY `id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Id';
--
-- AUTO_INCREMENT for table `salesrule_coupon_aggregated_updated`
--
ALTER TABLE `salesrule_coupon_aggregated_updated`
  MODIFY `id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Id';
--
-- AUTO_INCREMENT for table `salesrule_customer`
--
ALTER TABLE `salesrule_customer`
  MODIFY `rule_customer_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Rule Customer Id';
--
-- AUTO_INCREMENT for table `salesrule_label`
--
ALTER TABLE `salesrule_label`
  MODIFY `label_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Label Id';
--
-- AUTO_INCREMENT for table `sales_bestsellers_aggregated_daily`
--
ALTER TABLE `sales_bestsellers_aggregated_daily`
  MODIFY `id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Id';
--
-- AUTO_INCREMENT for table `sales_bestsellers_aggregated_monthly`
--
ALTER TABLE `sales_bestsellers_aggregated_monthly`
  MODIFY `id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Id';
--
-- AUTO_INCREMENT for table `sales_bestsellers_aggregated_yearly`
--
ALTER TABLE `sales_bestsellers_aggregated_yearly`
  MODIFY `id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Id';
--
-- AUTO_INCREMENT for table `sales_creditmemo`
--
ALTER TABLE `sales_creditmemo`
  MODIFY `entity_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Entity Id';
--
-- AUTO_INCREMENT for table `sales_creditmemo_comment`
--
ALTER TABLE `sales_creditmemo_comment`
  MODIFY `entity_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Entity Id';
--
-- AUTO_INCREMENT for table `sales_creditmemo_item`
--
ALTER TABLE `sales_creditmemo_item`
  MODIFY `entity_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Entity Id';
--
-- AUTO_INCREMENT for table `sales_invoice`
--
ALTER TABLE `sales_invoice`
  MODIFY `entity_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Entity Id';
--
-- AUTO_INCREMENT for table `sales_invoiced_aggregated`
--
ALTER TABLE `sales_invoiced_aggregated`
  MODIFY `id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Id';
--
-- AUTO_INCREMENT for table `sales_invoiced_aggregated_order`
--
ALTER TABLE `sales_invoiced_aggregated_order`
  MODIFY `id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Id';
--
-- AUTO_INCREMENT for table `sales_invoice_comment`
--
ALTER TABLE `sales_invoice_comment`
  MODIFY `entity_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Entity Id';
--
-- AUTO_INCREMENT for table `sales_invoice_item`
--
ALTER TABLE `sales_invoice_item`
  MODIFY `entity_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Entity Id';
--
-- AUTO_INCREMENT for table `sales_order`
--
ALTER TABLE `sales_order`
  MODIFY `entity_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Entity Id', AUTO_INCREMENT=5;
--
-- AUTO_INCREMENT for table `sales_order_address`
--
ALTER TABLE `sales_order_address`
  MODIFY `entity_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Entity Id', AUTO_INCREMENT=5;
--
-- AUTO_INCREMENT for table `sales_order_aggregated_created`
--
ALTER TABLE `sales_order_aggregated_created`
  MODIFY `id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Id';
--
-- AUTO_INCREMENT for table `sales_order_aggregated_updated`
--
ALTER TABLE `sales_order_aggregated_updated`
  MODIFY `id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Id';
--
-- AUTO_INCREMENT for table `sales_order_item`
--
ALTER TABLE `sales_order_item`
  MODIFY `item_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Item Id', AUTO_INCREMENT=11;
--
-- AUTO_INCREMENT for table `sales_order_payment`
--
ALTER TABLE `sales_order_payment`
  MODIFY `entity_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Entity Id', AUTO_INCREMENT=5;
--
-- AUTO_INCREMENT for table `sales_order_status_history`
--
ALTER TABLE `sales_order_status_history`
  MODIFY `entity_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Entity Id';
--
-- AUTO_INCREMENT for table `sales_order_tax`
--
ALTER TABLE `sales_order_tax`
  MODIFY `tax_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Tax Id';
--
-- AUTO_INCREMENT for table `sales_order_tax_item`
--
ALTER TABLE `sales_order_tax_item`
  MODIFY `tax_item_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Tax Item Id';
--
-- AUTO_INCREMENT for table `sales_payment_transaction`
--
ALTER TABLE `sales_payment_transaction`
  MODIFY `transaction_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Transaction Id';
--
-- AUTO_INCREMENT for table `sales_refunded_aggregated`
--
ALTER TABLE `sales_refunded_aggregated`
  MODIFY `id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Id';
--
-- AUTO_INCREMENT for table `sales_refunded_aggregated_order`
--
ALTER TABLE `sales_refunded_aggregated_order`
  MODIFY `id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Id';
--
-- AUTO_INCREMENT for table `sales_sequence_meta`
--
ALTER TABLE `sales_sequence_meta`
  MODIFY `meta_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Id', AUTO_INCREMENT=13;
--
-- AUTO_INCREMENT for table `sales_sequence_profile`
--
ALTER TABLE `sales_sequence_profile`
  MODIFY `profile_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Id', AUTO_INCREMENT=13;
--
-- AUTO_INCREMENT for table `sales_shipment`
--
ALTER TABLE `sales_shipment`
  MODIFY `entity_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Entity Id';
--
-- AUTO_INCREMENT for table `sales_shipment_comment`
--
ALTER TABLE `sales_shipment_comment`
  MODIFY `entity_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Entity Id';
--
-- AUTO_INCREMENT for table `sales_shipment_item`
--
ALTER TABLE `sales_shipment_item`
  MODIFY `entity_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Entity Id';
--
-- AUTO_INCREMENT for table `sales_shipment_track`
--
ALTER TABLE `sales_shipment_track`
  MODIFY `entity_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Entity Id';
--
-- AUTO_INCREMENT for table `sales_shipping_aggregated`
--
ALTER TABLE `sales_shipping_aggregated`
  MODIFY `id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Id';
--
-- AUTO_INCREMENT for table `sales_shipping_aggregated_order`
--
ALTER TABLE `sales_shipping_aggregated_order`
  MODIFY `id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Id';
--
-- AUTO_INCREMENT for table `search_query`
--
ALTER TABLE `search_query`
  MODIFY `query_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Query ID', AUTO_INCREMENT=25;
--
-- AUTO_INCREMENT for table `sendfriend_log`
--
ALTER TABLE `sendfriend_log`
  MODIFY `log_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Log ID';
--
-- AUTO_INCREMENT for table `sequence_creditmemo_0`
--
ALTER TABLE `sequence_creditmemo_0`
  MODIFY `sequence_value` int(10) UNSIGNED NOT NULL AUTO_INCREMENT;
--
-- AUTO_INCREMENT for table `sequence_creditmemo_1`
--
ALTER TABLE `sequence_creditmemo_1`
  MODIFY `sequence_value` int(10) UNSIGNED NOT NULL AUTO_INCREMENT;
--
-- AUTO_INCREMENT for table `sequence_creditmemo_2`
--
ALTER TABLE `sequence_creditmemo_2`
  MODIFY `sequence_value` int(10) UNSIGNED NOT NULL AUTO_INCREMENT;
--
-- AUTO_INCREMENT for table `sequence_invoice_0`
--
ALTER TABLE `sequence_invoice_0`
  MODIFY `sequence_value` int(10) UNSIGNED NOT NULL AUTO_INCREMENT;
--
-- AUTO_INCREMENT for table `sequence_invoice_1`
--
ALTER TABLE `sequence_invoice_1`
  MODIFY `sequence_value` int(10) UNSIGNED NOT NULL AUTO_INCREMENT;
--
-- AUTO_INCREMENT for table `sequence_invoice_2`
--
ALTER TABLE `sequence_invoice_2`
  MODIFY `sequence_value` int(10) UNSIGNED NOT NULL AUTO_INCREMENT;
--
-- AUTO_INCREMENT for table `sequence_order_0`
--
ALTER TABLE `sequence_order_0`
  MODIFY `sequence_value` int(10) UNSIGNED NOT NULL AUTO_INCREMENT;
--
-- AUTO_INCREMENT for table `sequence_order_1`
--
ALTER TABLE `sequence_order_1`
  MODIFY `sequence_value` int(10) UNSIGNED NOT NULL AUTO_INCREMENT, AUTO_INCREMENT=5;
--
-- AUTO_INCREMENT for table `sequence_order_2`
--
ALTER TABLE `sequence_order_2`
  MODIFY `sequence_value` int(10) UNSIGNED NOT NULL AUTO_INCREMENT;
--
-- AUTO_INCREMENT for table `sequence_shipment_0`
--
ALTER TABLE `sequence_shipment_0`
  MODIFY `sequence_value` int(10) UNSIGNED NOT NULL AUTO_INCREMENT;
--
-- AUTO_INCREMENT for table `sequence_shipment_1`
--
ALTER TABLE `sequence_shipment_1`
  MODIFY `sequence_value` int(10) UNSIGNED NOT NULL AUTO_INCREMENT;
--
-- AUTO_INCREMENT for table `sequence_shipment_2`
--
ALTER TABLE `sequence_shipment_2`
  MODIFY `sequence_value` int(10) UNSIGNED NOT NULL AUTO_INCREMENT;
--
-- AUTO_INCREMENT for table `shipping_tablerate`
--
ALTER TABLE `shipping_tablerate`
  MODIFY `pk` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Primary key';
--
-- AUTO_INCREMENT for table `sitemap`
--
ALTER TABLE `sitemap`
  MODIFY `sitemap_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Sitemap Id';
--
-- AUTO_INCREMENT for table `store`
--
ALTER TABLE `store`
  MODIFY `store_id` smallint(5) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Store Id', AUTO_INCREMENT=3;
--
-- AUTO_INCREMENT for table `store_group`
--
ALTER TABLE `store_group`
  MODIFY `group_id` smallint(5) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Group Id', AUTO_INCREMENT=2;
--
-- AUTO_INCREMENT for table `store_website`
--
ALTER TABLE `store_website`
  MODIFY `website_id` smallint(5) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Website Id', AUTO_INCREMENT=2;
--
-- AUTO_INCREMENT for table `tax_calculation`
--
ALTER TABLE `tax_calculation`
  MODIFY `tax_calculation_id` int(11) NOT NULL AUTO_INCREMENT COMMENT 'Tax Calculation Id';
--
-- AUTO_INCREMENT for table `tax_calculation_rate`
--
ALTER TABLE `tax_calculation_rate`
  MODIFY `tax_calculation_rate_id` int(11) NOT NULL AUTO_INCREMENT COMMENT 'Tax Calculation Rate Id', AUTO_INCREMENT=3;
--
-- AUTO_INCREMENT for table `tax_calculation_rate_title`
--
ALTER TABLE `tax_calculation_rate_title`
  MODIFY `tax_calculation_rate_title_id` int(11) NOT NULL AUTO_INCREMENT COMMENT 'Tax Calculation Rate Title Id';
--
-- AUTO_INCREMENT for table `tax_calculation_rule`
--
ALTER TABLE `tax_calculation_rule`
  MODIFY `tax_calculation_rule_id` int(11) NOT NULL AUTO_INCREMENT COMMENT 'Tax Calculation Rule Id';
--
-- AUTO_INCREMENT for table `tax_class`
--
ALTER TABLE `tax_class`
  MODIFY `class_id` smallint(6) NOT NULL AUTO_INCREMENT COMMENT 'Class Id', AUTO_INCREMENT=4;
--
-- AUTO_INCREMENT for table `tax_order_aggregated_created`
--
ALTER TABLE `tax_order_aggregated_created`
  MODIFY `id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Id';
--
-- AUTO_INCREMENT for table `tax_order_aggregated_updated`
--
ALTER TABLE `tax_order_aggregated_updated`
  MODIFY `id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Id';
--
-- AUTO_INCREMENT for table `theme`
--
ALTER TABLE `theme`
  MODIFY `theme_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Theme identifier', AUTO_INCREMENT=5;
--
-- AUTO_INCREMENT for table `theme_file`
--
ALTER TABLE `theme_file`
  MODIFY `theme_files_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Theme files identifier';
--
-- AUTO_INCREMENT for table `translation`
--
ALTER TABLE `translation`
  MODIFY `key_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Key Id of Translation';
--
-- AUTO_INCREMENT for table `ui_bookmark`
--
ALTER TABLE `ui_bookmark`
  MODIFY `bookmark_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Bookmark identifier', AUTO_INCREMENT=9;
--
-- AUTO_INCREMENT for table `url_rewrite`
--
ALTER TABLE `url_rewrite`
  MODIFY `url_rewrite_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Rewrite Id', AUTO_INCREMENT=99;
--
-- AUTO_INCREMENT for table `variable`
--
ALTER TABLE `variable`
  MODIFY `variable_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Variable Id';
--
-- AUTO_INCREMENT for table `variable_value`
--
ALTER TABLE `variable_value`
  MODIFY `value_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Variable Value Id';
--
-- AUTO_INCREMENT for table `weee_tax`
--
ALTER TABLE `weee_tax`
  MODIFY `value_id` int(11) NOT NULL AUTO_INCREMENT COMMENT 'Value Id';
--
-- AUTO_INCREMENT for table `widget`
--
ALTER TABLE `widget`
  MODIFY `widget_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Widget Id';
--
-- AUTO_INCREMENT for table `widget_instance`
--
ALTER TABLE `widget_instance`
  MODIFY `instance_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Instance Id';
--
-- AUTO_INCREMENT for table `widget_instance_page`
--
ALTER TABLE `widget_instance_page`
  MODIFY `page_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Page Id';
--
-- AUTO_INCREMENT for table `wishlist`
--
ALTER TABLE `wishlist`
  MODIFY `wishlist_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Wishlist ID', AUTO_INCREMENT=2;
--
-- AUTO_INCREMENT for table `wishlist_item`
--
ALTER TABLE `wishlist_item`
  MODIFY `wishlist_item_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Wishlist item ID';
--
-- AUTO_INCREMENT for table `wishlist_item_option`
--
ALTER TABLE `wishlist_item_option`
  MODIFY `option_id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'Option Id';
--
-- Constraints for dumped tables
--

--
-- Constraints for table `admin_passwords`
--
ALTER TABLE `admin_passwords`
  ADD CONSTRAINT `ADMIN_PASSWORDS_USER_ID_ADMIN_USER_USER_ID` FOREIGN KEY (`user_id`) REFERENCES `admin_user` (`user_id`) ON DELETE CASCADE;

--
-- Constraints for table `authorization_rule`
--
ALTER TABLE `authorization_rule`
  ADD CONSTRAINT `AUTHORIZATION_RULE_ROLE_ID_AUTHORIZATION_ROLE_ROLE_ID` FOREIGN KEY (`role_id`) REFERENCES `authorization_role` (`role_id`) ON DELETE CASCADE;

--
-- Constraints for table `cataloginventory_stock_item`
--
ALTER TABLE `cataloginventory_stock_item`
  ADD CONSTRAINT `CATINV_STOCK_ITEM_PRD_ID_CAT_PRD_ENTT_ENTT_ID` FOREIGN KEY (`product_id`) REFERENCES `catalog_product_entity` (`entity_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `CATINV_STOCK_ITEM_STOCK_ID_CATINV_STOCK_STOCK_ID` FOREIGN KEY (`stock_id`) REFERENCES `cataloginventory_stock` (`stock_id`) ON DELETE CASCADE;

--
-- Constraints for table `catalogrule_customer_group`
--
ALTER TABLE `catalogrule_customer_group`
  ADD CONSTRAINT `CATALOGRULE_CUSTOMER_GROUP_RULE_ID_CATALOGRULE_RULE_ID` FOREIGN KEY (`rule_id`) REFERENCES `catalogrule` (`rule_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `CATRULE_CSTR_GROUP_CSTR_GROUP_ID_CSTR_GROUP_CSTR_GROUP_ID` FOREIGN KEY (`customer_group_id`) REFERENCES `customer_group` (`customer_group_id`) ON DELETE CASCADE;

--
-- Constraints for table `catalogrule_group_website`
--
ALTER TABLE `catalogrule_group_website`
  ADD CONSTRAINT `CATALOGRULE_GROUP_WEBSITE_RULE_ID_CATALOGRULE_RULE_ID` FOREIGN KEY (`rule_id`) REFERENCES `catalogrule` (`rule_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `CATALOGRULE_GROUP_WEBSITE_WEBSITE_ID_STORE_WEBSITE_WEBSITE_ID` FOREIGN KEY (`website_id`) REFERENCES `store_website` (`website_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `CATRULE_GROUP_WS_CSTR_GROUP_ID_CSTR_GROUP_CSTR_GROUP_ID` FOREIGN KEY (`customer_group_id`) REFERENCES `customer_group` (`customer_group_id`) ON DELETE CASCADE;

--
-- Constraints for table `catalogrule_website`
--
ALTER TABLE `catalogrule_website`
  ADD CONSTRAINT `CATALOGRULE_WEBSITE_RULE_ID_CATALOGRULE_RULE_ID` FOREIGN KEY (`rule_id`) REFERENCES `catalogrule` (`rule_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `CATALOGRULE_WEBSITE_WEBSITE_ID_STORE_WEBSITE_WEBSITE_ID` FOREIGN KEY (`website_id`) REFERENCES `store_website` (`website_id`) ON DELETE CASCADE;

--
-- Constraints for table `catalog_category_entity_datetime`
--
ALTER TABLE `catalog_category_entity_datetime`
  ADD CONSTRAINT `CATALOG_CATEGORY_ENTITY_DATETIME_STORE_ID_STORE_STORE_ID` FOREIGN KEY (`store_id`) REFERENCES `store` (`store_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `CAT_CTGR_ENTT_DTIME_ATTR_ID_EAV_ATTR_ATTR_ID` FOREIGN KEY (`attribute_id`) REFERENCES `eav_attribute` (`attribute_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `CAT_CTGR_ENTT_DTIME_ENTT_ID_CAT_CTGR_ENTT_ENTT_ID` FOREIGN KEY (`entity_id`) REFERENCES `catalog_category_entity` (`entity_id`) ON DELETE CASCADE;

--
-- Constraints for table `catalog_category_entity_decimal`
--
ALTER TABLE `catalog_category_entity_decimal`
  ADD CONSTRAINT `CATALOG_CATEGORY_ENTITY_DECIMAL_STORE_ID_STORE_STORE_ID` FOREIGN KEY (`store_id`) REFERENCES `store` (`store_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `CAT_CTGR_ENTT_DEC_ATTR_ID_EAV_ATTR_ATTR_ID` FOREIGN KEY (`attribute_id`) REFERENCES `eav_attribute` (`attribute_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `CAT_CTGR_ENTT_DEC_ENTT_ID_CAT_CTGR_ENTT_ENTT_ID` FOREIGN KEY (`entity_id`) REFERENCES `catalog_category_entity` (`entity_id`) ON DELETE CASCADE;

--
-- Constraints for table `catalog_category_entity_int`
--
ALTER TABLE `catalog_category_entity_int`
  ADD CONSTRAINT `CATALOG_CATEGORY_ENTITY_INT_STORE_ID_STORE_STORE_ID` FOREIGN KEY (`store_id`) REFERENCES `store` (`store_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `CAT_CTGR_ENTT_INT_ATTR_ID_EAV_ATTR_ATTR_ID` FOREIGN KEY (`attribute_id`) REFERENCES `eav_attribute` (`attribute_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `CAT_CTGR_ENTT_INT_ENTT_ID_CAT_CTGR_ENTT_ENTT_ID` FOREIGN KEY (`entity_id`) REFERENCES `catalog_category_entity` (`entity_id`) ON DELETE CASCADE;

--
-- Constraints for table `catalog_category_entity_text`
--
ALTER TABLE `catalog_category_entity_text`
  ADD CONSTRAINT `CATALOG_CATEGORY_ENTITY_TEXT_STORE_ID_STORE_STORE_ID` FOREIGN KEY (`store_id`) REFERENCES `store` (`store_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `CAT_CTGR_ENTT_TEXT_ATTR_ID_EAV_ATTR_ATTR_ID` FOREIGN KEY (`attribute_id`) REFERENCES `eav_attribute` (`attribute_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `CAT_CTGR_ENTT_TEXT_ENTT_ID_CAT_CTGR_ENTT_ENTT_ID` FOREIGN KEY (`entity_id`) REFERENCES `catalog_category_entity` (`entity_id`) ON DELETE CASCADE;

--
-- Constraints for table `catalog_category_entity_varchar`
--
ALTER TABLE `catalog_category_entity_varchar`
  ADD CONSTRAINT `CATALOG_CATEGORY_ENTITY_VARCHAR_STORE_ID_STORE_STORE_ID` FOREIGN KEY (`store_id`) REFERENCES `store` (`store_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `CAT_CTGR_ENTT_VCHR_ATTR_ID_EAV_ATTR_ATTR_ID` FOREIGN KEY (`attribute_id`) REFERENCES `eav_attribute` (`attribute_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `CAT_CTGR_ENTT_VCHR_ENTT_ID_CAT_CTGR_ENTT_ENTT_ID` FOREIGN KEY (`entity_id`) REFERENCES `catalog_category_entity` (`entity_id`) ON DELETE CASCADE;

--
-- Constraints for table `catalog_category_product`
--
ALTER TABLE `catalog_category_product`
  ADD CONSTRAINT `CAT_CTGR_PRD_CTGR_ID_CAT_CTGR_ENTT_ENTT_ID` FOREIGN KEY (`category_id`) REFERENCES `catalog_category_entity` (`entity_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `CAT_CTGR_PRD_PRD_ID_CAT_PRD_ENTT_ENTT_ID` FOREIGN KEY (`product_id`) REFERENCES `catalog_product_entity` (`entity_id`) ON DELETE CASCADE;

--
-- Constraints for table `catalog_compare_item`
--
ALTER TABLE `catalog_compare_item`
  ADD CONSTRAINT `CATALOG_COMPARE_ITEM_CUSTOMER_ID_CUSTOMER_ENTITY_ENTITY_ID` FOREIGN KEY (`customer_id`) REFERENCES `customer_entity` (`entity_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `CATALOG_COMPARE_ITEM_PRODUCT_ID_CATALOG_PRODUCT_ENTITY_ENTITY_ID` FOREIGN KEY (`product_id`) REFERENCES `catalog_product_entity` (`entity_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `CATALOG_COMPARE_ITEM_STORE_ID_STORE_STORE_ID` FOREIGN KEY (`store_id`) REFERENCES `store` (`store_id`) ON DELETE SET NULL;

--
-- Constraints for table `catalog_eav_attribute`
--
ALTER TABLE `catalog_eav_attribute`
  ADD CONSTRAINT `CATALOG_EAV_ATTRIBUTE_ATTRIBUTE_ID_EAV_ATTRIBUTE_ATTRIBUTE_ID` FOREIGN KEY (`attribute_id`) REFERENCES `eav_attribute` (`attribute_id`) ON DELETE CASCADE;

--
-- Constraints for table `catalog_product_bundle_option`
--
ALTER TABLE `catalog_product_bundle_option`
  ADD CONSTRAINT `CAT_PRD_BNDL_OPT_PARENT_ID_CAT_PRD_ENTT_ENTT_ID` FOREIGN KEY (`parent_id`) REFERENCES `catalog_product_entity` (`entity_id`) ON DELETE CASCADE;

--
-- Constraints for table `catalog_product_bundle_option_value`
--
ALTER TABLE `catalog_product_bundle_option_value`
  ADD CONSTRAINT `CAT_PRD_BNDL_OPT_VAL_OPT_ID_CAT_PRD_BNDL_OPT_OPT_ID` FOREIGN KEY (`option_id`) REFERENCES `catalog_product_bundle_option` (`option_id`) ON DELETE CASCADE;

--
-- Constraints for table `catalog_product_bundle_price_index`
--
ALTER TABLE `catalog_product_bundle_price_index`
  ADD CONSTRAINT `CAT_PRD_BNDL_PRICE_IDX_CSTR_GROUP_ID_CSTR_GROUP_CSTR_GROUP_ID` FOREIGN KEY (`customer_group_id`) REFERENCES `customer_group` (`customer_group_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `CAT_PRD_BNDL_PRICE_IDX_ENTT_ID_CAT_PRD_ENTT_ENTT_ID` FOREIGN KEY (`entity_id`) REFERENCES `catalog_product_entity` (`entity_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `CAT_PRD_BNDL_PRICE_IDX_WS_ID_STORE_WS_WS_ID` FOREIGN KEY (`website_id`) REFERENCES `store_website` (`website_id`) ON DELETE CASCADE;

--
-- Constraints for table `catalog_product_bundle_selection`
--
ALTER TABLE `catalog_product_bundle_selection`
  ADD CONSTRAINT `CAT_PRD_BNDL_SELECTION_OPT_ID_CAT_PRD_BNDL_OPT_OPT_ID` FOREIGN KEY (`option_id`) REFERENCES `catalog_product_bundle_option` (`option_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `CAT_PRD_BNDL_SELECTION_PRD_ID_CAT_PRD_ENTT_ENTT_ID` FOREIGN KEY (`product_id`) REFERENCES `catalog_product_entity` (`entity_id`) ON DELETE CASCADE;

--
-- Constraints for table `catalog_product_bundle_selection_price`
--
ALTER TABLE `catalog_product_bundle_selection_price`
  ADD CONSTRAINT `CAT_PRD_BNDL_SELECTION_PRICE_WS_ID_STORE_WS_WS_ID` FOREIGN KEY (`website_id`) REFERENCES `store_website` (`website_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `FK_DCF37523AA05D770A70AA4ED7C2616E4` FOREIGN KEY (`selection_id`) REFERENCES `catalog_product_bundle_selection` (`selection_id`) ON DELETE CASCADE;

--
-- Constraints for table `catalog_product_entity`
--
ALTER TABLE `catalog_product_entity`
  ADD CONSTRAINT `CAT_PRD_ENTT_ATTR_SET_ID_EAV_ATTR_SET_ATTR_SET_ID` FOREIGN KEY (`attribute_set_id`) REFERENCES `eav_attribute_set` (`attribute_set_id`) ON DELETE CASCADE;

--
-- Constraints for table `catalog_product_entity_datetime`
--
ALTER TABLE `catalog_product_entity_datetime`
  ADD CONSTRAINT `CATALOG_PRODUCT_ENTITY_DATETIME_STORE_ID_STORE_STORE_ID` FOREIGN KEY (`store_id`) REFERENCES `store` (`store_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `CAT_PRD_ENTT_DTIME_ATTR_ID_EAV_ATTR_ATTR_ID` FOREIGN KEY (`attribute_id`) REFERENCES `eav_attribute` (`attribute_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `CAT_PRD_ENTT_DTIME_ENTT_ID_CAT_PRD_ENTT_ENTT_ID` FOREIGN KEY (`entity_id`) REFERENCES `catalog_product_entity` (`entity_id`) ON DELETE CASCADE;

--
-- Constraints for table `catalog_product_entity_decimal`
--
ALTER TABLE `catalog_product_entity_decimal`
  ADD CONSTRAINT `CATALOG_PRODUCT_ENTITY_DECIMAL_STORE_ID_STORE_STORE_ID` FOREIGN KEY (`store_id`) REFERENCES `store` (`store_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `CAT_PRD_ENTT_DEC_ATTR_ID_EAV_ATTR_ATTR_ID` FOREIGN KEY (`attribute_id`) REFERENCES `eav_attribute` (`attribute_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `CAT_PRD_ENTT_DEC_ENTT_ID_CAT_PRD_ENTT_ENTT_ID` FOREIGN KEY (`entity_id`) REFERENCES `catalog_product_entity` (`entity_id`) ON DELETE CASCADE;

--
-- Constraints for table `catalog_product_entity_gallery`
--
ALTER TABLE `catalog_product_entity_gallery`
  ADD CONSTRAINT `CATALOG_PRODUCT_ENTITY_GALLERY_STORE_ID_STORE_STORE_ID` FOREIGN KEY (`store_id`) REFERENCES `store` (`store_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `CAT_PRD_ENTT_GLR_ATTR_ID_EAV_ATTR_ATTR_ID` FOREIGN KEY (`attribute_id`) REFERENCES `eav_attribute` (`attribute_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `CAT_PRD_ENTT_GLR_ENTT_ID_CAT_PRD_ENTT_ENTT_ID` FOREIGN KEY (`entity_id`) REFERENCES `catalog_product_entity` (`entity_id`) ON DELETE CASCADE;

--
-- Constraints for table `catalog_product_entity_int`
--
ALTER TABLE `catalog_product_entity_int`
  ADD CONSTRAINT `CATALOG_PRODUCT_ENTITY_INT_STORE_ID_STORE_STORE_ID` FOREIGN KEY (`store_id`) REFERENCES `store` (`store_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `CAT_PRD_ENTT_INT_ATTR_ID_EAV_ATTR_ATTR_ID` FOREIGN KEY (`attribute_id`) REFERENCES `eav_attribute` (`attribute_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `CAT_PRD_ENTT_INT_ENTT_ID_CAT_PRD_ENTT_ENTT_ID` FOREIGN KEY (`entity_id`) REFERENCES `catalog_product_entity` (`entity_id`) ON DELETE CASCADE;

--
-- Constraints for table `catalog_product_entity_media_gallery`
--
ALTER TABLE `catalog_product_entity_media_gallery`
  ADD CONSTRAINT `CAT_PRD_ENTT_MDA_GLR_ATTR_ID_EAV_ATTR_ATTR_ID` FOREIGN KEY (`attribute_id`) REFERENCES `eav_attribute` (`attribute_id`) ON DELETE CASCADE;

--
-- Constraints for table `catalog_product_entity_media_gallery_value`
--
ALTER TABLE `catalog_product_entity_media_gallery_value`
  ADD CONSTRAINT `CAT_PRD_ENTT_MDA_GLR_VAL_ENTT_ID_CAT_PRD_ENTT_ENTT_ID` FOREIGN KEY (`entity_id`) REFERENCES `catalog_product_entity` (`entity_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `CAT_PRD_ENTT_MDA_GLR_VAL_STORE_ID_STORE_STORE_ID` FOREIGN KEY (`store_id`) REFERENCES `store` (`store_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `CAT_PRD_ENTT_MDA_GLR_VAL_VAL_ID_CAT_PRD_ENTT_MDA_GLR_VAL_ID` FOREIGN KEY (`value_id`) REFERENCES `catalog_product_entity_media_gallery` (`value_id`) ON DELETE CASCADE;

--
-- Constraints for table `catalog_product_entity_media_gallery_value_to_entity`
--
ALTER TABLE `catalog_product_entity_media_gallery_value_to_entity`
  ADD CONSTRAINT `CAT_PRD_ENTT_MDA_GLR_VAL_TO_ENTT_ENTT_ID_CAT_PRD_ENTT_ENTT_ID` FOREIGN KEY (`entity_id`) REFERENCES `catalog_product_entity` (`entity_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `FK_A6C6C8FAA386736921D3A7C4B50B1185` FOREIGN KEY (`value_id`) REFERENCES `catalog_product_entity_media_gallery` (`value_id`) ON DELETE CASCADE;

--
-- Constraints for table `catalog_product_entity_media_gallery_value_video`
--
ALTER TABLE `catalog_product_entity_media_gallery_value_video`
  ADD CONSTRAINT `CAT_PRD_ENTT_MDA_GLR_VAL_VIDEO_STORE_ID_STORE_STORE_ID` FOREIGN KEY (`store_id`) REFERENCES `store` (`store_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `FK_6FDF205946906B0E653E60AA769899F8` FOREIGN KEY (`value_id`) REFERENCES `catalog_product_entity_media_gallery` (`value_id`) ON DELETE CASCADE;

--
-- Constraints for table `catalog_product_entity_text`
--
ALTER TABLE `catalog_product_entity_text`
  ADD CONSTRAINT `CATALOG_PRODUCT_ENTITY_TEXT_STORE_ID_STORE_STORE_ID` FOREIGN KEY (`store_id`) REFERENCES `store` (`store_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `CAT_PRD_ENTT_TEXT_ATTR_ID_EAV_ATTR_ATTR_ID` FOREIGN KEY (`attribute_id`) REFERENCES `eav_attribute` (`attribute_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `CAT_PRD_ENTT_TEXT_ENTT_ID_CAT_PRD_ENTT_ENTT_ID` FOREIGN KEY (`entity_id`) REFERENCES `catalog_product_entity` (`entity_id`) ON DELETE CASCADE;

--
-- Constraints for table `catalog_product_entity_tier_price`
--
ALTER TABLE `catalog_product_entity_tier_price`
  ADD CONSTRAINT `CAT_PRD_ENTT_TIER_PRICE_CSTR_GROUP_ID_CSTR_GROUP_CSTR_GROUP_ID` FOREIGN KEY (`customer_group_id`) REFERENCES `customer_group` (`customer_group_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `CAT_PRD_ENTT_TIER_PRICE_ENTT_ID_CAT_PRD_ENTT_ENTT_ID` FOREIGN KEY (`entity_id`) REFERENCES `catalog_product_entity` (`entity_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `CAT_PRD_ENTT_TIER_PRICE_WS_ID_STORE_WS_WS_ID` FOREIGN KEY (`website_id`) REFERENCES `store_website` (`website_id`) ON DELETE CASCADE;

--
-- Constraints for table `catalog_product_entity_varchar`
--
ALTER TABLE `catalog_product_entity_varchar`
  ADD CONSTRAINT `CATALOG_PRODUCT_ENTITY_VARCHAR_STORE_ID_STORE_STORE_ID` FOREIGN KEY (`store_id`) REFERENCES `store` (`store_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `CAT_PRD_ENTT_VCHR_ATTR_ID_EAV_ATTR_ATTR_ID` FOREIGN KEY (`attribute_id`) REFERENCES `eav_attribute` (`attribute_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `CAT_PRD_ENTT_VCHR_ENTT_ID_CAT_PRD_ENTT_ENTT_ID` FOREIGN KEY (`entity_id`) REFERENCES `catalog_product_entity` (`entity_id`) ON DELETE CASCADE;

--
-- Constraints for table `catalog_product_index_price`
--
ALTER TABLE `catalog_product_index_price`
  ADD CONSTRAINT `CATALOG_PRODUCT_INDEX_PRICE_WEBSITE_ID_STORE_WEBSITE_WEBSITE_ID` FOREIGN KEY (`website_id`) REFERENCES `store_website` (`website_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `CAT_PRD_IDX_PRICE_CSTR_GROUP_ID_CSTR_GROUP_CSTR_GROUP_ID` FOREIGN KEY (`customer_group_id`) REFERENCES `customer_group` (`customer_group_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `CAT_PRD_IDX_PRICE_ENTT_ID_CAT_PRD_ENTT_ENTT_ID` FOREIGN KEY (`entity_id`) REFERENCES `catalog_product_entity` (`entity_id`) ON DELETE CASCADE;

--
-- Constraints for table `catalog_product_index_tier_price`
--
ALTER TABLE `catalog_product_index_tier_price`
  ADD CONSTRAINT `CAT_PRD_IDX_TIER_PRICE_CSTR_GROUP_ID_CSTR_GROUP_CSTR_GROUP_ID` FOREIGN KEY (`customer_group_id`) REFERENCES `customer_group` (`customer_group_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `CAT_PRD_IDX_TIER_PRICE_ENTT_ID_CAT_PRD_ENTT_ENTT_ID` FOREIGN KEY (`entity_id`) REFERENCES `catalog_product_entity` (`entity_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `CAT_PRD_IDX_TIER_PRICE_WS_ID_STORE_WS_WS_ID` FOREIGN KEY (`website_id`) REFERENCES `store_website` (`website_id`) ON DELETE CASCADE;

--
-- Constraints for table `catalog_product_index_website`
--
ALTER TABLE `catalog_product_index_website`
  ADD CONSTRAINT `CAT_PRD_IDX_WS_WS_ID_STORE_WS_WS_ID` FOREIGN KEY (`website_id`) REFERENCES `store_website` (`website_id`) ON DELETE CASCADE;

--
-- Constraints for table `catalog_product_link`
--
ALTER TABLE `catalog_product_link`
  ADD CONSTRAINT `CATALOG_PRODUCT_LINK_PRODUCT_ID_CATALOG_PRODUCT_ENTITY_ENTITY_ID` FOREIGN KEY (`product_id`) REFERENCES `catalog_product_entity` (`entity_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `CAT_PRD_LNK_LNKED_PRD_ID_CAT_PRD_ENTT_ENTT_ID` FOREIGN KEY (`linked_product_id`) REFERENCES `catalog_product_entity` (`entity_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `CAT_PRD_LNK_LNK_TYPE_ID_CAT_PRD_LNK_TYPE_LNK_TYPE_ID` FOREIGN KEY (`link_type_id`) REFERENCES `catalog_product_link_type` (`link_type_id`) ON DELETE CASCADE;

--
-- Constraints for table `catalog_product_link_attribute`
--
ALTER TABLE `catalog_product_link_attribute`
  ADD CONSTRAINT `CAT_PRD_LNK_ATTR_LNK_TYPE_ID_CAT_PRD_LNK_TYPE_LNK_TYPE_ID` FOREIGN KEY (`link_type_id`) REFERENCES `catalog_product_link_type` (`link_type_id`) ON DELETE CASCADE;

--
-- Constraints for table `catalog_product_link_attribute_decimal`
--
ALTER TABLE `catalog_product_link_attribute_decimal`
  ADD CONSTRAINT `CAT_PRD_LNK_ATTR_DEC_LNK_ID_CAT_PRD_LNK_LNK_ID` FOREIGN KEY (`link_id`) REFERENCES `catalog_product_link` (`link_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `FK_AB2EFA9A14F7BCF1D5400056203D14B6` FOREIGN KEY (`product_link_attribute_id`) REFERENCES `catalog_product_link_attribute` (`product_link_attribute_id`) ON DELETE CASCADE;

--
-- Constraints for table `catalog_product_link_attribute_int`
--
ALTER TABLE `catalog_product_link_attribute_int`
  ADD CONSTRAINT `CAT_PRD_LNK_ATTR_INT_LNK_ID_CAT_PRD_LNK_LNK_ID` FOREIGN KEY (`link_id`) REFERENCES `catalog_product_link` (`link_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `FK_D6D878F8BA2A4282F8DDED7E6E3DE35C` FOREIGN KEY (`product_link_attribute_id`) REFERENCES `catalog_product_link_attribute` (`product_link_attribute_id`) ON DELETE CASCADE;

--
-- Constraints for table `catalog_product_link_attribute_varchar`
--
ALTER TABLE `catalog_product_link_attribute_varchar`
  ADD CONSTRAINT `CAT_PRD_LNK_ATTR_VCHR_LNK_ID_CAT_PRD_LNK_LNK_ID` FOREIGN KEY (`link_id`) REFERENCES `catalog_product_link` (`link_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `FK_DEE9C4DA61CFCC01DFCF50F0D79CEA51` FOREIGN KEY (`product_link_attribute_id`) REFERENCES `catalog_product_link_attribute` (`product_link_attribute_id`) ON DELETE CASCADE;

--
-- Constraints for table `catalog_product_option`
--
ALTER TABLE `catalog_product_option`
  ADD CONSTRAINT `CAT_PRD_OPT_PRD_ID_CAT_PRD_ENTT_ENTT_ID` FOREIGN KEY (`product_id`) REFERENCES `catalog_product_entity` (`entity_id`) ON DELETE CASCADE;

--
-- Constraints for table `catalog_product_option_price`
--
ALTER TABLE `catalog_product_option_price`
  ADD CONSTRAINT `CATALOG_PRODUCT_OPTION_PRICE_STORE_ID_STORE_STORE_ID` FOREIGN KEY (`store_id`) REFERENCES `store` (`store_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `CAT_PRD_OPT_PRICE_OPT_ID_CAT_PRD_OPT_OPT_ID` FOREIGN KEY (`option_id`) REFERENCES `catalog_product_option` (`option_id`) ON DELETE CASCADE;

--
-- Constraints for table `catalog_product_option_title`
--
ALTER TABLE `catalog_product_option_title`
  ADD CONSTRAINT `CATALOG_PRODUCT_OPTION_TITLE_STORE_ID_STORE_STORE_ID` FOREIGN KEY (`store_id`) REFERENCES `store` (`store_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `CAT_PRD_OPT_TTL_OPT_ID_CAT_PRD_OPT_OPT_ID` FOREIGN KEY (`option_id`) REFERENCES `catalog_product_option` (`option_id`) ON DELETE CASCADE;

--
-- Constraints for table `catalog_product_option_type_price`
--
ALTER TABLE `catalog_product_option_type_price`
  ADD CONSTRAINT `CATALOG_PRODUCT_OPTION_TYPE_PRICE_STORE_ID_STORE_STORE_ID` FOREIGN KEY (`store_id`) REFERENCES `store` (`store_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `FK_B523E3378E8602F376CC415825576B7F` FOREIGN KEY (`option_type_id`) REFERENCES `catalog_product_option_type_value` (`option_type_id`) ON DELETE CASCADE;

--
-- Constraints for table `catalog_product_option_type_title`
--
ALTER TABLE `catalog_product_option_type_title`
  ADD CONSTRAINT `CATALOG_PRODUCT_OPTION_TYPE_TITLE_STORE_ID_STORE_STORE_ID` FOREIGN KEY (`store_id`) REFERENCES `store` (`store_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `FK_C085B9CF2C2A302E8043FDEA1937D6A2` FOREIGN KEY (`option_type_id`) REFERENCES `catalog_product_option_type_value` (`option_type_id`) ON DELETE CASCADE;

--
-- Constraints for table `catalog_product_option_type_value`
--
ALTER TABLE `catalog_product_option_type_value`
  ADD CONSTRAINT `CAT_PRD_OPT_TYPE_VAL_OPT_ID_CAT_PRD_OPT_OPT_ID` FOREIGN KEY (`option_id`) REFERENCES `catalog_product_option` (`option_id`) ON DELETE CASCADE;

--
-- Constraints for table `catalog_product_relation`
--
ALTER TABLE `catalog_product_relation`
  ADD CONSTRAINT `CAT_PRD_RELATION_CHILD_ID_CAT_PRD_ENTT_ENTT_ID` FOREIGN KEY (`child_id`) REFERENCES `catalog_product_entity` (`entity_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `CAT_PRD_RELATION_PARENT_ID_CAT_PRD_ENTT_ENTT_ID` FOREIGN KEY (`parent_id`) REFERENCES `catalog_product_entity` (`entity_id`) ON DELETE CASCADE;

--
-- Constraints for table `catalog_product_super_attribute`
--
ALTER TABLE `catalog_product_super_attribute`
  ADD CONSTRAINT `CAT_PRD_SPR_ATTR_PRD_ID_CAT_PRD_ENTT_ENTT_ID` FOREIGN KEY (`product_id`) REFERENCES `catalog_product_entity` (`entity_id`) ON DELETE CASCADE;

--
-- Constraints for table `catalog_product_super_attribute_label`
--
ALTER TABLE `catalog_product_super_attribute_label`
  ADD CONSTRAINT `CATALOG_PRODUCT_SUPER_ATTRIBUTE_LABEL_STORE_ID_STORE_STORE_ID` FOREIGN KEY (`store_id`) REFERENCES `store` (`store_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `FK_309442281DF7784210ED82B2CC51E5D5` FOREIGN KEY (`product_super_attribute_id`) REFERENCES `catalog_product_super_attribute` (`product_super_attribute_id`) ON DELETE CASCADE;

--
-- Constraints for table `catalog_product_super_link`
--
ALTER TABLE `catalog_product_super_link`
  ADD CONSTRAINT `CAT_PRD_SPR_LNK_PARENT_ID_CAT_PRD_ENTT_ENTT_ID` FOREIGN KEY (`parent_id`) REFERENCES `catalog_product_entity` (`entity_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `CAT_PRD_SPR_LNK_PRD_ID_CAT_PRD_ENTT_ENTT_ID` FOREIGN KEY (`product_id`) REFERENCES `catalog_product_entity` (`entity_id`) ON DELETE CASCADE;

--
-- Constraints for table `catalog_product_website`
--
ALTER TABLE `catalog_product_website`
  ADD CONSTRAINT `CATALOG_PRODUCT_WEBSITE_WEBSITE_ID_STORE_WEBSITE_WEBSITE_ID` FOREIGN KEY (`website_id`) REFERENCES `store_website` (`website_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `CAT_PRD_WS_PRD_ID_CAT_PRD_ENTT_ENTT_ID` FOREIGN KEY (`product_id`) REFERENCES `catalog_product_entity` (`entity_id`) ON DELETE CASCADE;

--
-- Constraints for table `catalog_url_rewrite_product_category`
--
ALTER TABLE `catalog_url_rewrite_product_category`
  ADD CONSTRAINT `CAT_URL_REWRITE_PRD_CTGR_CTGR_ID_CAT_CTGR_ENTT_ENTT_ID` FOREIGN KEY (`category_id`) REFERENCES `catalog_category_entity` (`entity_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `CAT_URL_REWRITE_PRD_CTGR_PRD_ID_CAT_PRD_ENTT_ENTT_ID` FOREIGN KEY (`product_id`) REFERENCES `catalog_product_entity` (`entity_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `FK_BB79E64705D7F17FE181F23144528FC8` FOREIGN KEY (`url_rewrite_id`) REFERENCES `url_rewrite` (`url_rewrite_id`) ON DELETE CASCADE;

--
-- Constraints for table `checkout_agreement_store`
--
ALTER TABLE `checkout_agreement_store`
  ADD CONSTRAINT `CHECKOUT_AGREEMENT_STORE_STORE_ID_STORE_STORE_ID` FOREIGN KEY (`store_id`) REFERENCES `store` (`store_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `CHKT_AGRT_STORE_AGRT_ID_CHKT_AGRT_AGRT_ID` FOREIGN KEY (`agreement_id`) REFERENCES `checkout_agreement` (`agreement_id`) ON DELETE CASCADE;

--
-- Constraints for table `cms_block_store`
--
ALTER TABLE `cms_block_store`
  ADD CONSTRAINT `CMS_BLOCK_STORE_BLOCK_ID_CMS_BLOCK_BLOCK_ID` FOREIGN KEY (`block_id`) REFERENCES `cms_block` (`block_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `CMS_BLOCK_STORE_STORE_ID_STORE_STORE_ID` FOREIGN KEY (`store_id`) REFERENCES `store` (`store_id`) ON DELETE CASCADE;

--
-- Constraints for table `cms_page_store`
--
ALTER TABLE `cms_page_store`
  ADD CONSTRAINT `CMS_PAGE_STORE_PAGE_ID_CMS_PAGE_PAGE_ID` FOREIGN KEY (`page_id`) REFERENCES `cms_page` (`page_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `CMS_PAGE_STORE_STORE_ID_STORE_STORE_ID` FOREIGN KEY (`store_id`) REFERENCES `store` (`store_id`) ON DELETE CASCADE;

--
-- Constraints for table `customer_address_entity`
--
ALTER TABLE `customer_address_entity`
  ADD CONSTRAINT `CUSTOMER_ADDRESS_ENTITY_PARENT_ID_CUSTOMER_ENTITY_ENTITY_ID` FOREIGN KEY (`parent_id`) REFERENCES `customer_entity` (`entity_id`) ON DELETE CASCADE;

--
-- Constraints for table `customer_address_entity_datetime`
--
ALTER TABLE `customer_address_entity_datetime`
  ADD CONSTRAINT `CSTR_ADDR_ENTT_DTIME_ATTR_ID_EAV_ATTR_ATTR_ID` FOREIGN KEY (`attribute_id`) REFERENCES `eav_attribute` (`attribute_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `CSTR_ADDR_ENTT_DTIME_ENTT_ID_CSTR_ADDR_ENTT_ENTT_ID` FOREIGN KEY (`entity_id`) REFERENCES `customer_address_entity` (`entity_id`) ON DELETE CASCADE;

--
-- Constraints for table `customer_address_entity_decimal`
--
ALTER TABLE `customer_address_entity_decimal`
  ADD CONSTRAINT `CSTR_ADDR_ENTT_DEC_ATTR_ID_EAV_ATTR_ATTR_ID` FOREIGN KEY (`attribute_id`) REFERENCES `eav_attribute` (`attribute_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `CSTR_ADDR_ENTT_DEC_ENTT_ID_CSTR_ADDR_ENTT_ENTT_ID` FOREIGN KEY (`entity_id`) REFERENCES `customer_address_entity` (`entity_id`) ON DELETE CASCADE;

--
-- Constraints for table `customer_address_entity_int`
--
ALTER TABLE `customer_address_entity_int`
  ADD CONSTRAINT `CSTR_ADDR_ENTT_INT_ATTR_ID_EAV_ATTR_ATTR_ID` FOREIGN KEY (`attribute_id`) REFERENCES `eav_attribute` (`attribute_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `CSTR_ADDR_ENTT_INT_ENTT_ID_CSTR_ADDR_ENTT_ENTT_ID` FOREIGN KEY (`entity_id`) REFERENCES `customer_address_entity` (`entity_id`) ON DELETE CASCADE;

--
-- Constraints for table `customer_address_entity_text`
--
ALTER TABLE `customer_address_entity_text`
  ADD CONSTRAINT `CSTR_ADDR_ENTT_TEXT_ATTR_ID_EAV_ATTR_ATTR_ID` FOREIGN KEY (`attribute_id`) REFERENCES `eav_attribute` (`attribute_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `CSTR_ADDR_ENTT_TEXT_ENTT_ID_CSTR_ADDR_ENTT_ENTT_ID` FOREIGN KEY (`entity_id`) REFERENCES `customer_address_entity` (`entity_id`) ON DELETE CASCADE;

--
-- Constraints for table `customer_address_entity_varchar`
--
ALTER TABLE `customer_address_entity_varchar`
  ADD CONSTRAINT `CSTR_ADDR_ENTT_VCHR_ATTR_ID_EAV_ATTR_ATTR_ID` FOREIGN KEY (`attribute_id`) REFERENCES `eav_attribute` (`attribute_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `CSTR_ADDR_ENTT_VCHR_ENTT_ID_CSTR_ADDR_ENTT_ENTT_ID` FOREIGN KEY (`entity_id`) REFERENCES `customer_address_entity` (`entity_id`) ON DELETE CASCADE;

--
-- Constraints for table `customer_eav_attribute`
--
ALTER TABLE `customer_eav_attribute`
  ADD CONSTRAINT `CUSTOMER_EAV_ATTRIBUTE_ATTRIBUTE_ID_EAV_ATTRIBUTE_ATTRIBUTE_ID` FOREIGN KEY (`attribute_id`) REFERENCES `eav_attribute` (`attribute_id`) ON DELETE CASCADE;

--
-- Constraints for table `customer_eav_attribute_website`
--
ALTER TABLE `customer_eav_attribute_website`
  ADD CONSTRAINT `CSTR_EAV_ATTR_WS_ATTR_ID_EAV_ATTR_ATTR_ID` FOREIGN KEY (`attribute_id`) REFERENCES `eav_attribute` (`attribute_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `CSTR_EAV_ATTR_WS_WS_ID_STORE_WS_WS_ID` FOREIGN KEY (`website_id`) REFERENCES `store_website` (`website_id`) ON DELETE CASCADE;

--
-- Constraints for table `customer_entity`
--
ALTER TABLE `customer_entity`
  ADD CONSTRAINT `CUSTOMER_ENTITY_STORE_ID_STORE_STORE_ID` FOREIGN KEY (`store_id`) REFERENCES `store` (`store_id`) ON DELETE SET NULL,
  ADD CONSTRAINT `CUSTOMER_ENTITY_WEBSITE_ID_STORE_WEBSITE_WEBSITE_ID` FOREIGN KEY (`website_id`) REFERENCES `store_website` (`website_id`) ON DELETE SET NULL;

--
-- Constraints for table `customer_entity_datetime`
--
ALTER TABLE `customer_entity_datetime`
  ADD CONSTRAINT `CUSTOMER_ENTITY_DATETIME_ATTRIBUTE_ID_EAV_ATTRIBUTE_ATTRIBUTE_ID` FOREIGN KEY (`attribute_id`) REFERENCES `eav_attribute` (`attribute_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `CUSTOMER_ENTITY_DATETIME_ENTITY_ID_CUSTOMER_ENTITY_ENTITY_ID` FOREIGN KEY (`entity_id`) REFERENCES `customer_entity` (`entity_id`) ON DELETE CASCADE;

--
-- Constraints for table `customer_entity_decimal`
--
ALTER TABLE `customer_entity_decimal`
  ADD CONSTRAINT `CUSTOMER_ENTITY_DECIMAL_ATTRIBUTE_ID_EAV_ATTRIBUTE_ATTRIBUTE_ID` FOREIGN KEY (`attribute_id`) REFERENCES `eav_attribute` (`attribute_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `CUSTOMER_ENTITY_DECIMAL_ENTITY_ID_CUSTOMER_ENTITY_ENTITY_ID` FOREIGN KEY (`entity_id`) REFERENCES `customer_entity` (`entity_id`) ON DELETE CASCADE;

--
-- Constraints for table `customer_entity_int`
--
ALTER TABLE `customer_entity_int`
  ADD CONSTRAINT `CUSTOMER_ENTITY_INT_ATTRIBUTE_ID_EAV_ATTRIBUTE_ATTRIBUTE_ID` FOREIGN KEY (`attribute_id`) REFERENCES `eav_attribute` (`attribute_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `CUSTOMER_ENTITY_INT_ENTITY_ID_CUSTOMER_ENTITY_ENTITY_ID` FOREIGN KEY (`entity_id`) REFERENCES `customer_entity` (`entity_id`) ON DELETE CASCADE;

--
-- Constraints for table `customer_entity_text`
--
ALTER TABLE `customer_entity_text`
  ADD CONSTRAINT `CUSTOMER_ENTITY_TEXT_ATTRIBUTE_ID_EAV_ATTRIBUTE_ATTRIBUTE_ID` FOREIGN KEY (`attribute_id`) REFERENCES `eav_attribute` (`attribute_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `CUSTOMER_ENTITY_TEXT_ENTITY_ID_CUSTOMER_ENTITY_ENTITY_ID` FOREIGN KEY (`entity_id`) REFERENCES `customer_entity` (`entity_id`) ON DELETE CASCADE;

--
-- Constraints for table `customer_entity_varchar`
--
ALTER TABLE `customer_entity_varchar`
  ADD CONSTRAINT `CUSTOMER_ENTITY_VARCHAR_ATTRIBUTE_ID_EAV_ATTRIBUTE_ATTRIBUTE_ID` FOREIGN KEY (`attribute_id`) REFERENCES `eav_attribute` (`attribute_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `CUSTOMER_ENTITY_VARCHAR_ENTITY_ID_CUSTOMER_ENTITY_ENTITY_ID` FOREIGN KEY (`entity_id`) REFERENCES `customer_entity` (`entity_id`) ON DELETE CASCADE;

--
-- Constraints for table `customer_form_attribute`
--
ALTER TABLE `customer_form_attribute`
  ADD CONSTRAINT `CUSTOMER_FORM_ATTRIBUTE_ATTRIBUTE_ID_EAV_ATTRIBUTE_ATTRIBUTE_ID` FOREIGN KEY (`attribute_id`) REFERENCES `eav_attribute` (`attribute_id`) ON DELETE CASCADE;

--
-- Constraints for table `design_change`
--
ALTER TABLE `design_change`
  ADD CONSTRAINT `DESIGN_CHANGE_STORE_ID_STORE_STORE_ID` FOREIGN KEY (`store_id`) REFERENCES `store` (`store_id`) ON DELETE CASCADE;

--
-- Constraints for table `directory_country_region_name`
--
ALTER TABLE `directory_country_region_name`
  ADD CONSTRAINT `DIR_COUNTRY_REGION_NAME_REGION_ID_DIR_COUNTRY_REGION_REGION_ID` FOREIGN KEY (`region_id`) REFERENCES `directory_country_region` (`region_id`) ON DELETE CASCADE;

--
-- Constraints for table `downloadable_link`
--
ALTER TABLE `downloadable_link`
  ADD CONSTRAINT `DOWNLOADABLE_LINK_PRODUCT_ID_CATALOG_PRODUCT_ENTITY_ENTITY_ID` FOREIGN KEY (`product_id`) REFERENCES `catalog_product_entity` (`entity_id`) ON DELETE CASCADE;

--
-- Constraints for table `downloadable_link_price`
--
ALTER TABLE `downloadable_link_price`
  ADD CONSTRAINT `DOWNLOADABLE_LINK_PRICE_LINK_ID_DOWNLOADABLE_LINK_LINK_ID` FOREIGN KEY (`link_id`) REFERENCES `downloadable_link` (`link_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `DOWNLOADABLE_LINK_PRICE_WEBSITE_ID_STORE_WEBSITE_WEBSITE_ID` FOREIGN KEY (`website_id`) REFERENCES `store_website` (`website_id`) ON DELETE CASCADE;

--
-- Constraints for table `downloadable_link_purchased`
--
ALTER TABLE `downloadable_link_purchased`
  ADD CONSTRAINT `DL_LNK_PURCHASED_CSTR_ID_CSTR_ENTT_ENTT_ID` FOREIGN KEY (`customer_id`) REFERENCES `customer_entity` (`entity_id`) ON DELETE SET NULL,
  ADD CONSTRAINT `DOWNLOADABLE_LINK_PURCHASED_ORDER_ID_SALES_ORDER_ENTITY_ID` FOREIGN KEY (`order_id`) REFERENCES `sales_order` (`entity_id`) ON DELETE SET NULL;

--
-- Constraints for table `downloadable_link_purchased_item`
--
ALTER TABLE `downloadable_link_purchased_item`
  ADD CONSTRAINT `DL_LNK_PURCHASED_ITEM_ORDER_ITEM_ID_SALES_ORDER_ITEM_ITEM_ID` FOREIGN KEY (`order_item_id`) REFERENCES `sales_order_item` (`item_id`) ON DELETE SET NULL,
  ADD CONSTRAINT `DL_LNK_PURCHASED_ITEM_PURCHASED_ID_DL_LNK_PURCHASED_PURCHASED_ID` FOREIGN KEY (`purchased_id`) REFERENCES `downloadable_link_purchased` (`purchased_id`) ON DELETE CASCADE;

--
-- Constraints for table `downloadable_link_title`
--
ALTER TABLE `downloadable_link_title`
  ADD CONSTRAINT `DOWNLOADABLE_LINK_TITLE_LINK_ID_DOWNLOADABLE_LINK_LINK_ID` FOREIGN KEY (`link_id`) REFERENCES `downloadable_link` (`link_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `DOWNLOADABLE_LINK_TITLE_STORE_ID_STORE_STORE_ID` FOREIGN KEY (`store_id`) REFERENCES `store` (`store_id`) ON DELETE CASCADE;

--
-- Constraints for table `downloadable_sample`
--
ALTER TABLE `downloadable_sample`
  ADD CONSTRAINT `DOWNLOADABLE_SAMPLE_PRODUCT_ID_CATALOG_PRODUCT_ENTITY_ENTITY_ID` FOREIGN KEY (`product_id`) REFERENCES `catalog_product_entity` (`entity_id`) ON DELETE CASCADE;

--
-- Constraints for table `downloadable_sample_title`
--
ALTER TABLE `downloadable_sample_title`
  ADD CONSTRAINT `DL_SAMPLE_TTL_SAMPLE_ID_DL_SAMPLE_SAMPLE_ID` FOREIGN KEY (`sample_id`) REFERENCES `downloadable_sample` (`sample_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `DOWNLOADABLE_SAMPLE_TITLE_STORE_ID_STORE_STORE_ID` FOREIGN KEY (`store_id`) REFERENCES `store` (`store_id`) ON DELETE CASCADE;

--
-- Constraints for table `eav_attribute`
--
ALTER TABLE `eav_attribute`
  ADD CONSTRAINT `EAV_ATTRIBUTE_ENTITY_TYPE_ID_EAV_ENTITY_TYPE_ENTITY_TYPE_ID` FOREIGN KEY (`entity_type_id`) REFERENCES `eav_entity_type` (`entity_type_id`) ON DELETE CASCADE;

--
-- Constraints for table `eav_attribute_group`
--
ALTER TABLE `eav_attribute_group`
  ADD CONSTRAINT `EAV_ATTR_GROUP_ATTR_SET_ID_EAV_ATTR_SET_ATTR_SET_ID` FOREIGN KEY (`attribute_set_id`) REFERENCES `eav_attribute_set` (`attribute_set_id`) ON DELETE CASCADE;

--
-- Constraints for table `eav_attribute_label`
--
ALTER TABLE `eav_attribute_label`
  ADD CONSTRAINT `EAV_ATTRIBUTE_LABEL_ATTRIBUTE_ID_EAV_ATTRIBUTE_ATTRIBUTE_ID` FOREIGN KEY (`attribute_id`) REFERENCES `eav_attribute` (`attribute_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `EAV_ATTRIBUTE_LABEL_STORE_ID_STORE_STORE_ID` FOREIGN KEY (`store_id`) REFERENCES `store` (`store_id`) ON DELETE CASCADE;

--
-- Constraints for table `eav_attribute_option`
--
ALTER TABLE `eav_attribute_option`
  ADD CONSTRAINT `EAV_ATTRIBUTE_OPTION_ATTRIBUTE_ID_EAV_ATTRIBUTE_ATTRIBUTE_ID` FOREIGN KEY (`attribute_id`) REFERENCES `eav_attribute` (`attribute_id`) ON DELETE CASCADE;

--
-- Constraints for table `eav_attribute_option_swatch`
--
ALTER TABLE `eav_attribute_option_swatch`
  ADD CONSTRAINT `EAV_ATTRIBUTE_OPTION_SWATCH_STORE_ID_STORE_STORE_ID` FOREIGN KEY (`store_id`) REFERENCES `store` (`store_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `EAV_ATTR_OPT_SWATCH_OPT_ID_EAV_ATTR_OPT_OPT_ID` FOREIGN KEY (`option_id`) REFERENCES `eav_attribute_option` (`option_id`) ON DELETE CASCADE;

--
-- Constraints for table `eav_attribute_option_value`
--
ALTER TABLE `eav_attribute_option_value`
  ADD CONSTRAINT `EAV_ATTRIBUTE_OPTION_VALUE_STORE_ID_STORE_STORE_ID` FOREIGN KEY (`store_id`) REFERENCES `store` (`store_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `EAV_ATTR_OPT_VAL_OPT_ID_EAV_ATTR_OPT_OPT_ID` FOREIGN KEY (`option_id`) REFERENCES `eav_attribute_option` (`option_id`) ON DELETE CASCADE;

--
-- Constraints for table `eav_attribute_set`
--
ALTER TABLE `eav_attribute_set`
  ADD CONSTRAINT `EAV_ATTRIBUTE_SET_ENTITY_TYPE_ID_EAV_ENTITY_TYPE_ENTITY_TYPE_ID` FOREIGN KEY (`entity_type_id`) REFERENCES `eav_entity_type` (`entity_type_id`) ON DELETE CASCADE;

--
-- Constraints for table `eav_entity`
--
ALTER TABLE `eav_entity`
  ADD CONSTRAINT `EAV_ENTITY_ENTITY_TYPE_ID_EAV_ENTITY_TYPE_ENTITY_TYPE_ID` FOREIGN KEY (`entity_type_id`) REFERENCES `eav_entity_type` (`entity_type_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `EAV_ENTITY_STORE_ID_STORE_STORE_ID` FOREIGN KEY (`store_id`) REFERENCES `store` (`store_id`) ON DELETE CASCADE;

--
-- Constraints for table `eav_entity_attribute`
--
ALTER TABLE `eav_entity_attribute`
  ADD CONSTRAINT `EAV_ENTITY_ATTRIBUTE_ATTRIBUTE_ID_EAV_ATTRIBUTE_ATTRIBUTE_ID` FOREIGN KEY (`attribute_id`) REFERENCES `eav_attribute` (`attribute_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `EAV_ENTT_ATTR_ATTR_GROUP_ID_EAV_ATTR_GROUP_ATTR_GROUP_ID` FOREIGN KEY (`attribute_group_id`) REFERENCES `eav_attribute_group` (`attribute_group_id`) ON DELETE CASCADE;

--
-- Constraints for table `eav_entity_datetime`
--
ALTER TABLE `eav_entity_datetime`
  ADD CONSTRAINT `EAV_ENTITY_DATETIME_ENTITY_ID_EAV_ENTITY_ENTITY_ID` FOREIGN KEY (`entity_id`) REFERENCES `eav_entity` (`entity_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `EAV_ENTITY_DATETIME_STORE_ID_STORE_STORE_ID` FOREIGN KEY (`store_id`) REFERENCES `store` (`store_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `EAV_ENTT_DTIME_ENTT_TYPE_ID_EAV_ENTT_TYPE_ENTT_TYPE_ID` FOREIGN KEY (`entity_type_id`) REFERENCES `eav_entity_type` (`entity_type_id`) ON DELETE CASCADE;

--
-- Constraints for table `eav_entity_decimal`
--
ALTER TABLE `eav_entity_decimal`
  ADD CONSTRAINT `EAV_ENTITY_DECIMAL_ENTITY_ID_EAV_ENTITY_ENTITY_ID` FOREIGN KEY (`entity_id`) REFERENCES `eav_entity` (`entity_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `EAV_ENTITY_DECIMAL_ENTITY_TYPE_ID_EAV_ENTITY_TYPE_ENTITY_TYPE_ID` FOREIGN KEY (`entity_type_id`) REFERENCES `eav_entity_type` (`entity_type_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `EAV_ENTITY_DECIMAL_STORE_ID_STORE_STORE_ID` FOREIGN KEY (`store_id`) REFERENCES `store` (`store_id`) ON DELETE CASCADE;

--
-- Constraints for table `eav_entity_int`
--
ALTER TABLE `eav_entity_int`
  ADD CONSTRAINT `EAV_ENTITY_INT_ENTITY_ID_EAV_ENTITY_ENTITY_ID` FOREIGN KEY (`entity_id`) REFERENCES `eav_entity` (`entity_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `EAV_ENTITY_INT_ENTITY_TYPE_ID_EAV_ENTITY_TYPE_ENTITY_TYPE_ID` FOREIGN KEY (`entity_type_id`) REFERENCES `eav_entity_type` (`entity_type_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `EAV_ENTITY_INT_STORE_ID_STORE_STORE_ID` FOREIGN KEY (`store_id`) REFERENCES `store` (`store_id`) ON DELETE CASCADE;

--
-- Constraints for table `eav_entity_store`
--
ALTER TABLE `eav_entity_store`
  ADD CONSTRAINT `EAV_ENTITY_STORE_ENTITY_TYPE_ID_EAV_ENTITY_TYPE_ENTITY_TYPE_ID` FOREIGN KEY (`entity_type_id`) REFERENCES `eav_entity_type` (`entity_type_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `EAV_ENTITY_STORE_STORE_ID_STORE_STORE_ID` FOREIGN KEY (`store_id`) REFERENCES `store` (`store_id`) ON DELETE CASCADE;

--
-- Constraints for table `eav_entity_text`
--
ALTER TABLE `eav_entity_text`
  ADD CONSTRAINT `EAV_ENTITY_TEXT_ENTITY_ID_EAV_ENTITY_ENTITY_ID` FOREIGN KEY (`entity_id`) REFERENCES `eav_entity` (`entity_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `EAV_ENTITY_TEXT_ENTITY_TYPE_ID_EAV_ENTITY_TYPE_ENTITY_TYPE_ID` FOREIGN KEY (`entity_type_id`) REFERENCES `eav_entity_type` (`entity_type_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `EAV_ENTITY_TEXT_STORE_ID_STORE_STORE_ID` FOREIGN KEY (`store_id`) REFERENCES `store` (`store_id`) ON DELETE CASCADE;

--
-- Constraints for table `eav_entity_varchar`
--
ALTER TABLE `eav_entity_varchar`
  ADD CONSTRAINT `EAV_ENTITY_VARCHAR_ENTITY_ID_EAV_ENTITY_ENTITY_ID` FOREIGN KEY (`entity_id`) REFERENCES `eav_entity` (`entity_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `EAV_ENTITY_VARCHAR_ENTITY_TYPE_ID_EAV_ENTITY_TYPE_ENTITY_TYPE_ID` FOREIGN KEY (`entity_type_id`) REFERENCES `eav_entity_type` (`entity_type_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `EAV_ENTITY_VARCHAR_STORE_ID_STORE_STORE_ID` FOREIGN KEY (`store_id`) REFERENCES `store` (`store_id`) ON DELETE CASCADE;

--
-- Constraints for table `eav_form_element`
--
ALTER TABLE `eav_form_element`
  ADD CONSTRAINT `EAV_FORM_ELEMENT_ATTRIBUTE_ID_EAV_ATTRIBUTE_ATTRIBUTE_ID` FOREIGN KEY (`attribute_id`) REFERENCES `eav_attribute` (`attribute_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `EAV_FORM_ELEMENT_FIELDSET_ID_EAV_FORM_FIELDSET_FIELDSET_ID` FOREIGN KEY (`fieldset_id`) REFERENCES `eav_form_fieldset` (`fieldset_id`) ON DELETE SET NULL,
  ADD CONSTRAINT `EAV_FORM_ELEMENT_TYPE_ID_EAV_FORM_TYPE_TYPE_ID` FOREIGN KEY (`type_id`) REFERENCES `eav_form_type` (`type_id`) ON DELETE CASCADE;

--
-- Constraints for table `eav_form_fieldset`
--
ALTER TABLE `eav_form_fieldset`
  ADD CONSTRAINT `EAV_FORM_FIELDSET_TYPE_ID_EAV_FORM_TYPE_TYPE_ID` FOREIGN KEY (`type_id`) REFERENCES `eav_form_type` (`type_id`) ON DELETE CASCADE;

--
-- Constraints for table `eav_form_fieldset_label`
--
ALTER TABLE `eav_form_fieldset_label`
  ADD CONSTRAINT `EAV_FORM_FIELDSET_LABEL_STORE_ID_STORE_STORE_ID` FOREIGN KEY (`store_id`) REFERENCES `store` (`store_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `EAV_FORM_FSET_LBL_FSET_ID_EAV_FORM_FSET_FSET_ID` FOREIGN KEY (`fieldset_id`) REFERENCES `eav_form_fieldset` (`fieldset_id`) ON DELETE CASCADE;

--
-- Constraints for table `eav_form_type`
--
ALTER TABLE `eav_form_type`
  ADD CONSTRAINT `EAV_FORM_TYPE_STORE_ID_STORE_STORE_ID` FOREIGN KEY (`store_id`) REFERENCES `store` (`store_id`) ON DELETE CASCADE;

--
-- Constraints for table `eav_form_type_entity`
--
ALTER TABLE `eav_form_type_entity`
  ADD CONSTRAINT `EAV_FORM_TYPE_ENTITY_TYPE_ID_EAV_FORM_TYPE_TYPE_ID` FOREIGN KEY (`type_id`) REFERENCES `eav_form_type` (`type_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `EAV_FORM_TYPE_ENTT_ENTT_TYPE_ID_EAV_ENTT_TYPE_ENTT_TYPE_ID` FOREIGN KEY (`entity_type_id`) REFERENCES `eav_entity_type` (`entity_type_id`) ON DELETE CASCADE;

--
-- Constraints for table `googleoptimizer_code`
--
ALTER TABLE `googleoptimizer_code`
  ADD CONSTRAINT `GOOGLEOPTIMIZER_CODE_STORE_ID_STORE_STORE_ID` FOREIGN KEY (`store_id`) REFERENCES `store` (`store_id`) ON DELETE CASCADE;

--
-- Constraints for table `integration`
--
ALTER TABLE `integration`
  ADD CONSTRAINT `INTEGRATION_CONSUMER_ID_OAUTH_CONSUMER_ENTITY_ID` FOREIGN KEY (`consumer_id`) REFERENCES `oauth_consumer` (`entity_id`) ON DELETE CASCADE;

--
-- Constraints for table `layout_link`
--
ALTER TABLE `layout_link`
  ADD CONSTRAINT `LAYOUT_LINK_LAYOUT_UPDATE_ID_LAYOUT_UPDATE_LAYOUT_UPDATE_ID` FOREIGN KEY (`layout_update_id`) REFERENCES `layout_update` (`layout_update_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `LAYOUT_LINK_STORE_ID_STORE_STORE_ID` FOREIGN KEY (`store_id`) REFERENCES `store` (`store_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `LAYOUT_LINK_THEME_ID_THEME_THEME_ID` FOREIGN KEY (`theme_id`) REFERENCES `theme` (`theme_id`) ON DELETE CASCADE;

--
-- Constraints for table `newsletter_problem`
--
ALTER TABLE `newsletter_problem`
  ADD CONSTRAINT `NEWSLETTER_PROBLEM_QUEUE_ID_NEWSLETTER_QUEUE_QUEUE_ID` FOREIGN KEY (`queue_id`) REFERENCES `newsletter_queue` (`queue_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `NLTTR_PROBLEM_SUBSCRIBER_ID_NLTTR_SUBSCRIBER_SUBSCRIBER_ID` FOREIGN KEY (`subscriber_id`) REFERENCES `newsletter_subscriber` (`subscriber_id`) ON DELETE CASCADE;

--
-- Constraints for table `newsletter_queue`
--
ALTER TABLE `newsletter_queue`
  ADD CONSTRAINT `NEWSLETTER_QUEUE_TEMPLATE_ID_NEWSLETTER_TEMPLATE_TEMPLATE_ID` FOREIGN KEY (`template_id`) REFERENCES `newsletter_template` (`template_id`) ON DELETE CASCADE;

--
-- Constraints for table `newsletter_queue_link`
--
ALTER TABLE `newsletter_queue_link`
  ADD CONSTRAINT `NEWSLETTER_QUEUE_LINK_QUEUE_ID_NEWSLETTER_QUEUE_QUEUE_ID` FOREIGN KEY (`queue_id`) REFERENCES `newsletter_queue` (`queue_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `NLTTR_QUEUE_LNK_SUBSCRIBER_ID_NLTTR_SUBSCRIBER_SUBSCRIBER_ID` FOREIGN KEY (`subscriber_id`) REFERENCES `newsletter_subscriber` (`subscriber_id`) ON DELETE CASCADE;

--
-- Constraints for table `newsletter_queue_store_link`
--
ALTER TABLE `newsletter_queue_store_link`
  ADD CONSTRAINT `NEWSLETTER_QUEUE_STORE_LINK_QUEUE_ID_NEWSLETTER_QUEUE_QUEUE_ID` FOREIGN KEY (`queue_id`) REFERENCES `newsletter_queue` (`queue_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `NEWSLETTER_QUEUE_STORE_LINK_STORE_ID_STORE_STORE_ID` FOREIGN KEY (`store_id`) REFERENCES `store` (`store_id`) ON DELETE CASCADE;

--
-- Constraints for table `newsletter_subscriber`
--
ALTER TABLE `newsletter_subscriber`
  ADD CONSTRAINT `NEWSLETTER_SUBSCRIBER_STORE_ID_STORE_STORE_ID` FOREIGN KEY (`store_id`) REFERENCES `store` (`store_id`) ON DELETE SET NULL;

--
-- Constraints for table `oauth_nonce`
--
ALTER TABLE `oauth_nonce`
  ADD CONSTRAINT `OAUTH_NONCE_CONSUMER_ID_OAUTH_CONSUMER_ENTITY_ID` FOREIGN KEY (`consumer_id`) REFERENCES `oauth_consumer` (`entity_id`) ON DELETE CASCADE;

--
-- Constraints for table `oauth_token`
--
ALTER TABLE `oauth_token`
  ADD CONSTRAINT `OAUTH_TOKEN_ADMIN_ID_ADMIN_USER_USER_ID` FOREIGN KEY (`admin_id`) REFERENCES `admin_user` (`user_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `OAUTH_TOKEN_CONSUMER_ID_OAUTH_CONSUMER_ENTITY_ID` FOREIGN KEY (`consumer_id`) REFERENCES `oauth_consumer` (`entity_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `OAUTH_TOKEN_CUSTOMER_ID_CUSTOMER_ENTITY_ENTITY_ID` FOREIGN KEY (`customer_id`) REFERENCES `customer_entity` (`entity_id`) ON DELETE CASCADE;

--
-- Constraints for table `paypal_billing_agreement`
--
ALTER TABLE `paypal_billing_agreement`
  ADD CONSTRAINT `PAYPAL_BILLING_AGREEMENT_CUSTOMER_ID_CUSTOMER_ENTITY_ENTITY_ID` FOREIGN KEY (`customer_id`) REFERENCES `customer_entity` (`entity_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `PAYPAL_BILLING_AGREEMENT_STORE_ID_STORE_STORE_ID` FOREIGN KEY (`store_id`) REFERENCES `store` (`store_id`) ON DELETE SET NULL;

--
-- Constraints for table `paypal_billing_agreement_order`
--
ALTER TABLE `paypal_billing_agreement_order`
  ADD CONSTRAINT `PAYPAL_BILLING_AGREEMENT_ORDER_ORDER_ID_SALES_ORDER_ENTITY_ID` FOREIGN KEY (`order_id`) REFERENCES `sales_order` (`entity_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `PAYPAL_BILLING_AGRT_ORDER_AGRT_ID_PAYPAL_BILLING_AGRT_AGRT_ID` FOREIGN KEY (`agreement_id`) REFERENCES `paypal_billing_agreement` (`agreement_id`) ON DELETE CASCADE;

--
-- Constraints for table `paypal_cert`
--
ALTER TABLE `paypal_cert`
  ADD CONSTRAINT `PAYPAL_CERT_WEBSITE_ID_STORE_WEBSITE_WEBSITE_ID` FOREIGN KEY (`website_id`) REFERENCES `store_website` (`website_id`) ON DELETE CASCADE;

--
-- Constraints for table `paypal_settlement_report_row`
--
ALTER TABLE `paypal_settlement_report_row`
  ADD CONSTRAINT `FK_E183E488F593E0DE10C6EBFFEBAC9B55` FOREIGN KEY (`report_id`) REFERENCES `paypal_settlement_report` (`report_id`) ON DELETE CASCADE;

--
-- Constraints for table `persistent_session`
--
ALTER TABLE `persistent_session`
  ADD CONSTRAINT `PERSISTENT_SESSION_CUSTOMER_ID_CUSTOMER_ENTITY_ENTITY_ID` FOREIGN KEY (`customer_id`) REFERENCES `customer_entity` (`entity_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `PERSISTENT_SESSION_WEBSITE_ID_STORE_WEBSITE_WEBSITE_ID` FOREIGN KEY (`website_id`) REFERENCES `store_website` (`website_id`) ON DELETE CASCADE;

--
-- Constraints for table `product_alert_price`
--
ALTER TABLE `product_alert_price`
  ADD CONSTRAINT `PRODUCT_ALERT_PRICE_CUSTOMER_ID_CUSTOMER_ENTITY_ENTITY_ID` FOREIGN KEY (`customer_id`) REFERENCES `customer_entity` (`entity_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `PRODUCT_ALERT_PRICE_PRODUCT_ID_CATALOG_PRODUCT_ENTITY_ENTITY_ID` FOREIGN KEY (`product_id`) REFERENCES `catalog_product_entity` (`entity_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `PRODUCT_ALERT_PRICE_WEBSITE_ID_STORE_WEBSITE_WEBSITE_ID` FOREIGN KEY (`website_id`) REFERENCES `store_website` (`website_id`) ON DELETE CASCADE;

--
-- Constraints for table `product_alert_stock`
--
ALTER TABLE `product_alert_stock`
  ADD CONSTRAINT `PRODUCT_ALERT_STOCK_CUSTOMER_ID_CUSTOMER_ENTITY_ENTITY_ID` FOREIGN KEY (`customer_id`) REFERENCES `customer_entity` (`entity_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `PRODUCT_ALERT_STOCK_PRODUCT_ID_CATALOG_PRODUCT_ENTITY_ENTITY_ID` FOREIGN KEY (`product_id`) REFERENCES `catalog_product_entity` (`entity_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `PRODUCT_ALERT_STOCK_WEBSITE_ID_STORE_WEBSITE_WEBSITE_ID` FOREIGN KEY (`website_id`) REFERENCES `store_website` (`website_id`) ON DELETE CASCADE;

--
-- Constraints for table `quote`
--
ALTER TABLE `quote`
  ADD CONSTRAINT `QUOTE_STORE_ID_STORE_STORE_ID` FOREIGN KEY (`store_id`) REFERENCES `store` (`store_id`) ON DELETE CASCADE;

--
-- Constraints for table `quote_address`
--
ALTER TABLE `quote_address`
  ADD CONSTRAINT `QUOTE_ADDRESS_QUOTE_ID_QUOTE_ENTITY_ID` FOREIGN KEY (`quote_id`) REFERENCES `quote` (`entity_id`) ON DELETE CASCADE;

--
-- Constraints for table `quote_address_item`
--
ALTER TABLE `quote_address_item`
  ADD CONSTRAINT `QUOTE_ADDRESS_ITEM_QUOTE_ADDRESS_ID_QUOTE_ADDRESS_ADDRESS_ID` FOREIGN KEY (`quote_address_id`) REFERENCES `quote_address` (`address_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `QUOTE_ADDRESS_ITEM_QUOTE_ITEM_ID_QUOTE_ITEM_ITEM_ID` FOREIGN KEY (`quote_item_id`) REFERENCES `quote_item` (`item_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `QUOTE_ADDR_ITEM_PARENT_ITEM_ID_QUOTE_ADDR_ITEM_ADDR_ITEM_ID` FOREIGN KEY (`parent_item_id`) REFERENCES `quote_address_item` (`address_item_id`) ON DELETE CASCADE;

--
-- Constraints for table `quote_id_mask`
--
ALTER TABLE `quote_id_mask`
  ADD CONSTRAINT `QUOTE_ID_MASK_QUOTE_ID_QUOTE_ENTITY_ID` FOREIGN KEY (`quote_id`) REFERENCES `quote` (`entity_id`) ON DELETE CASCADE;

--
-- Constraints for table `quote_item`
--
ALTER TABLE `quote_item`
  ADD CONSTRAINT `QUOTE_ITEM_PARENT_ITEM_ID_QUOTE_ITEM_ITEM_ID` FOREIGN KEY (`parent_item_id`) REFERENCES `quote_item` (`item_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `QUOTE_ITEM_PRODUCT_ID_CATALOG_PRODUCT_ENTITY_ENTITY_ID` FOREIGN KEY (`product_id`) REFERENCES `catalog_product_entity` (`entity_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `QUOTE_ITEM_QUOTE_ID_QUOTE_ENTITY_ID` FOREIGN KEY (`quote_id`) REFERENCES `quote` (`entity_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `QUOTE_ITEM_STORE_ID_STORE_STORE_ID` FOREIGN KEY (`store_id`) REFERENCES `store` (`store_id`) ON DELETE SET NULL;

--
-- Constraints for table `quote_item_option`
--
ALTER TABLE `quote_item_option`
  ADD CONSTRAINT `QUOTE_ITEM_OPTION_ITEM_ID_QUOTE_ITEM_ITEM_ID` FOREIGN KEY (`item_id`) REFERENCES `quote_item` (`item_id`) ON DELETE CASCADE;

--
-- Constraints for table `quote_payment`
--
ALTER TABLE `quote_payment`
  ADD CONSTRAINT `QUOTE_PAYMENT_QUOTE_ID_QUOTE_ENTITY_ID` FOREIGN KEY (`quote_id`) REFERENCES `quote` (`entity_id`) ON DELETE CASCADE;

--
-- Constraints for table `quote_shipping_rate`
--
ALTER TABLE `quote_shipping_rate`
  ADD CONSTRAINT `QUOTE_SHIPPING_RATE_ADDRESS_ID_QUOTE_ADDRESS_ADDRESS_ID` FOREIGN KEY (`address_id`) REFERENCES `quote_address` (`address_id`) ON DELETE CASCADE;

--
-- Constraints for table `rating`
--
ALTER TABLE `rating`
  ADD CONSTRAINT `RATING_ENTITY_ID_RATING_ENTITY_ENTITY_ID` FOREIGN KEY (`entity_id`) REFERENCES `rating_entity` (`entity_id`) ON DELETE CASCADE;

--
-- Constraints for table `rating_option`
--
ALTER TABLE `rating_option`
  ADD CONSTRAINT `RATING_OPTION_RATING_ID_RATING_RATING_ID` FOREIGN KEY (`rating_id`) REFERENCES `rating` (`rating_id`) ON DELETE CASCADE;

--
-- Constraints for table `rating_option_vote`
--
ALTER TABLE `rating_option_vote`
  ADD CONSTRAINT `RATING_OPTION_VOTE_OPTION_ID_RATING_OPTION_OPTION_ID` FOREIGN KEY (`option_id`) REFERENCES `rating_option` (`option_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `RATING_OPTION_VOTE_REVIEW_ID_REVIEW_REVIEW_ID` FOREIGN KEY (`review_id`) REFERENCES `review` (`review_id`) ON DELETE CASCADE;

--
-- Constraints for table `rating_option_vote_aggregated`
--
ALTER TABLE `rating_option_vote_aggregated`
  ADD CONSTRAINT `RATING_OPTION_VOTE_AGGREGATED_RATING_ID_RATING_RATING_ID` FOREIGN KEY (`rating_id`) REFERENCES `rating` (`rating_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `RATING_OPTION_VOTE_AGGREGATED_STORE_ID_STORE_STORE_ID` FOREIGN KEY (`store_id`) REFERENCES `store` (`store_id`) ON DELETE CASCADE;

--
-- Constraints for table `rating_store`
--
ALTER TABLE `rating_store`
  ADD CONSTRAINT `RATING_STORE_RATING_ID_RATING_RATING_ID` FOREIGN KEY (`rating_id`) REFERENCES `rating` (`rating_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `RATING_STORE_STORE_ID_STORE_STORE_ID` FOREIGN KEY (`store_id`) REFERENCES `store` (`store_id`) ON DELETE CASCADE;

--
-- Constraints for table `rating_title`
--
ALTER TABLE `rating_title`
  ADD CONSTRAINT `RATING_TITLE_RATING_ID_RATING_RATING_ID` FOREIGN KEY (`rating_id`) REFERENCES `rating` (`rating_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `RATING_TITLE_STORE_ID_STORE_STORE_ID` FOREIGN KEY (`store_id`) REFERENCES `store` (`store_id`) ON DELETE CASCADE;

--
-- Constraints for table `report_compared_product_index`
--
ALTER TABLE `report_compared_product_index`
  ADD CONSTRAINT `REPORT_CMPD_PRD_IDX_CSTR_ID_CSTR_ENTT_ENTT_ID` FOREIGN KEY (`customer_id`) REFERENCES `customer_entity` (`entity_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `REPORT_CMPD_PRD_IDX_PRD_ID_CAT_PRD_ENTT_ENTT_ID` FOREIGN KEY (`product_id`) REFERENCES `catalog_product_entity` (`entity_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `REPORT_COMPARED_PRODUCT_INDEX_STORE_ID_STORE_STORE_ID` FOREIGN KEY (`store_id`) REFERENCES `store` (`store_id`) ON DELETE SET NULL;

--
-- Constraints for table `report_event`
--
ALTER TABLE `report_event`
  ADD CONSTRAINT `REPORT_EVENT_EVENT_TYPE_ID_REPORT_EVENT_TYPES_EVENT_TYPE_ID` FOREIGN KEY (`event_type_id`) REFERENCES `report_event_types` (`event_type_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `REPORT_EVENT_STORE_ID_STORE_STORE_ID` FOREIGN KEY (`store_id`) REFERENCES `store` (`store_id`) ON DELETE CASCADE;

--
-- Constraints for table `report_viewed_product_aggregated_daily`
--
ALTER TABLE `report_viewed_product_aggregated_daily`
  ADD CONSTRAINT `REPORT_VIEWED_PRD_AGGRED_DAILY_PRD_ID_CAT_PRD_ENTT_ENTT_ID` FOREIGN KEY (`product_id`) REFERENCES `catalog_product_entity` (`entity_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `REPORT_VIEWED_PRODUCT_AGGREGATED_DAILY_STORE_ID_STORE_STORE_ID` FOREIGN KEY (`store_id`) REFERENCES `store` (`store_id`) ON DELETE CASCADE;

--
-- Constraints for table `report_viewed_product_aggregated_monthly`
--
ALTER TABLE `report_viewed_product_aggregated_monthly`
  ADD CONSTRAINT `REPORT_VIEWED_PRD_AGGRED_MONTHLY_PRD_ID_CAT_PRD_ENTT_ENTT_ID` FOREIGN KEY (`product_id`) REFERENCES `catalog_product_entity` (`entity_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `REPORT_VIEWED_PRODUCT_AGGREGATED_MONTHLY_STORE_ID_STORE_STORE_ID` FOREIGN KEY (`store_id`) REFERENCES `store` (`store_id`) ON DELETE CASCADE;

--
-- Constraints for table `report_viewed_product_aggregated_yearly`
--
ALTER TABLE `report_viewed_product_aggregated_yearly`
  ADD CONSTRAINT `REPORT_VIEWED_PRD_AGGRED_YEARLY_PRD_ID_CAT_PRD_ENTT_ENTT_ID` FOREIGN KEY (`product_id`) REFERENCES `catalog_product_entity` (`entity_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `REPORT_VIEWED_PRODUCT_AGGREGATED_YEARLY_STORE_ID_STORE_STORE_ID` FOREIGN KEY (`store_id`) REFERENCES `store` (`store_id`) ON DELETE CASCADE;

--
-- Constraints for table `report_viewed_product_index`
--
ALTER TABLE `report_viewed_product_index`
  ADD CONSTRAINT `REPORT_VIEWED_PRD_IDX_CSTR_ID_CSTR_ENTT_ENTT_ID` FOREIGN KEY (`customer_id`) REFERENCES `customer_entity` (`entity_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `REPORT_VIEWED_PRD_IDX_PRD_ID_CAT_PRD_ENTT_ENTT_ID` FOREIGN KEY (`product_id`) REFERENCES `catalog_product_entity` (`entity_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `REPORT_VIEWED_PRODUCT_INDEX_STORE_ID_STORE_STORE_ID` FOREIGN KEY (`store_id`) REFERENCES `store` (`store_id`) ON DELETE SET NULL;

--
-- Constraints for table `review`
--
ALTER TABLE `review`
  ADD CONSTRAINT `REVIEW_ENTITY_ID_REVIEW_ENTITY_ENTITY_ID` FOREIGN KEY (`entity_id`) REFERENCES `review_entity` (`entity_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `REVIEW_STATUS_ID_REVIEW_STATUS_STATUS_ID` FOREIGN KEY (`status_id`) REFERENCES `review_status` (`status_id`) ON DELETE NO ACTION;

--
-- Constraints for table `review_detail`
--
ALTER TABLE `review_detail`
  ADD CONSTRAINT `REVIEW_DETAIL_CUSTOMER_ID_CUSTOMER_ENTITY_ENTITY_ID` FOREIGN KEY (`customer_id`) REFERENCES `customer_entity` (`entity_id`) ON DELETE SET NULL,
  ADD CONSTRAINT `REVIEW_DETAIL_REVIEW_ID_REVIEW_REVIEW_ID` FOREIGN KEY (`review_id`) REFERENCES `review` (`review_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `REVIEW_DETAIL_STORE_ID_STORE_STORE_ID` FOREIGN KEY (`store_id`) REFERENCES `store` (`store_id`) ON DELETE SET NULL;

--
-- Constraints for table `review_entity_summary`
--
ALTER TABLE `review_entity_summary`
  ADD CONSTRAINT `REVIEW_ENTITY_SUMMARY_STORE_ID_STORE_STORE_ID` FOREIGN KEY (`store_id`) REFERENCES `store` (`store_id`) ON DELETE CASCADE;

--
-- Constraints for table `review_store`
--
ALTER TABLE `review_store`
  ADD CONSTRAINT `REVIEW_STORE_REVIEW_ID_REVIEW_REVIEW_ID` FOREIGN KEY (`review_id`) REFERENCES `review` (`review_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `REVIEW_STORE_STORE_ID_STORE_STORE_ID` FOREIGN KEY (`store_id`) REFERENCES `store` (`store_id`) ON DELETE CASCADE;

--
-- Constraints for table `salesrule_coupon`
--
ALTER TABLE `salesrule_coupon`
  ADD CONSTRAINT `SALESRULE_COUPON_RULE_ID_SALESRULE_RULE_ID` FOREIGN KEY (`rule_id`) REFERENCES `salesrule` (`rule_id`) ON DELETE CASCADE;

--
-- Constraints for table `salesrule_coupon_aggregated`
--
ALTER TABLE `salesrule_coupon_aggregated`
  ADD CONSTRAINT `SALESRULE_COUPON_AGGREGATED_STORE_ID_STORE_STORE_ID` FOREIGN KEY (`store_id`) REFERENCES `store` (`store_id`) ON DELETE CASCADE;

--
-- Constraints for table `salesrule_coupon_aggregated_order`
--
ALTER TABLE `salesrule_coupon_aggregated_order`
  ADD CONSTRAINT `SALESRULE_COUPON_AGGREGATED_ORDER_STORE_ID_STORE_STORE_ID` FOREIGN KEY (`store_id`) REFERENCES `store` (`store_id`) ON DELETE CASCADE;

--
-- Constraints for table `salesrule_coupon_aggregated_updated`
--
ALTER TABLE `salesrule_coupon_aggregated_updated`
  ADD CONSTRAINT `SALESRULE_COUPON_AGGREGATED_UPDATED_STORE_ID_STORE_STORE_ID` FOREIGN KEY (`store_id`) REFERENCES `store` (`store_id`) ON DELETE CASCADE;

--
-- Constraints for table `salesrule_coupon_usage`
--
ALTER TABLE `salesrule_coupon_usage`
  ADD CONSTRAINT `SALESRULE_COUPON_USAGE_COUPON_ID_SALESRULE_COUPON_COUPON_ID` FOREIGN KEY (`coupon_id`) REFERENCES `salesrule_coupon` (`coupon_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `SALESRULE_COUPON_USAGE_CUSTOMER_ID_CUSTOMER_ENTITY_ENTITY_ID` FOREIGN KEY (`customer_id`) REFERENCES `customer_entity` (`entity_id`) ON DELETE CASCADE;

--
-- Constraints for table `salesrule_customer`
--
ALTER TABLE `salesrule_customer`
  ADD CONSTRAINT `SALESRULE_CUSTOMER_CUSTOMER_ID_CUSTOMER_ENTITY_ENTITY_ID` FOREIGN KEY (`customer_id`) REFERENCES `customer_entity` (`entity_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `SALESRULE_CUSTOMER_RULE_ID_SALESRULE_RULE_ID` FOREIGN KEY (`rule_id`) REFERENCES `salesrule` (`rule_id`) ON DELETE CASCADE;

--
-- Constraints for table `salesrule_customer_group`
--
ALTER TABLE `salesrule_customer_group`
  ADD CONSTRAINT `SALESRULE_CSTR_GROUP_CSTR_GROUP_ID_CSTR_GROUP_CSTR_GROUP_ID` FOREIGN KEY (`customer_group_id`) REFERENCES `customer_group` (`customer_group_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `SALESRULE_CUSTOMER_GROUP_RULE_ID_SALESRULE_RULE_ID` FOREIGN KEY (`rule_id`) REFERENCES `salesrule` (`rule_id`) ON DELETE CASCADE;

--
-- Constraints for table `salesrule_label`
--
ALTER TABLE `salesrule_label`
  ADD CONSTRAINT `SALESRULE_LABEL_RULE_ID_SALESRULE_RULE_ID` FOREIGN KEY (`rule_id`) REFERENCES `salesrule` (`rule_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `SALESRULE_LABEL_STORE_ID_STORE_STORE_ID` FOREIGN KEY (`store_id`) REFERENCES `store` (`store_id`) ON DELETE CASCADE;

--
-- Constraints for table `salesrule_product_attribute`
--
ALTER TABLE `salesrule_product_attribute`
  ADD CONSTRAINT `SALESRULE_PRD_ATTR_ATTR_ID_EAV_ATTR_ATTR_ID` FOREIGN KEY (`attribute_id`) REFERENCES `eav_attribute` (`attribute_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `SALESRULE_PRD_ATTR_CSTR_GROUP_ID_CSTR_GROUP_CSTR_GROUP_ID` FOREIGN KEY (`customer_group_id`) REFERENCES `customer_group` (`customer_group_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `SALESRULE_PRODUCT_ATTRIBUTE_RULE_ID_SALESRULE_RULE_ID` FOREIGN KEY (`rule_id`) REFERENCES `salesrule` (`rule_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `SALESRULE_PRODUCT_ATTRIBUTE_WEBSITE_ID_STORE_WEBSITE_WEBSITE_ID` FOREIGN KEY (`website_id`) REFERENCES `store_website` (`website_id`) ON DELETE CASCADE;

--
-- Constraints for table `salesrule_website`
--
ALTER TABLE `salesrule_website`
  ADD CONSTRAINT `SALESRULE_WEBSITE_RULE_ID_SALESRULE_RULE_ID` FOREIGN KEY (`rule_id`) REFERENCES `salesrule` (`rule_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `SALESRULE_WEBSITE_WEBSITE_ID_STORE_WEBSITE_WEBSITE_ID` FOREIGN KEY (`website_id`) REFERENCES `store_website` (`website_id`) ON DELETE CASCADE;

--
-- Constraints for table `sales_bestsellers_aggregated_daily`
--
ALTER TABLE `sales_bestsellers_aggregated_daily`
  ADD CONSTRAINT `SALES_BESTSELLERS_AGGRED_DAILY_PRD_ID_CAT_PRD_ENTT_ENTT_ID` FOREIGN KEY (`product_id`) REFERENCES `catalog_product_entity` (`entity_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `SALES_BESTSELLERS_AGGREGATED_DAILY_STORE_ID_STORE_STORE_ID` FOREIGN KEY (`store_id`) REFERENCES `store` (`store_id`) ON DELETE CASCADE;

--
-- Constraints for table `sales_bestsellers_aggregated_monthly`
--
ALTER TABLE `sales_bestsellers_aggregated_monthly`
  ADD CONSTRAINT `SALES_BESTSELLERS_AGGRED_MONTHLY_PRD_ID_CAT_PRD_ENTT_ENTT_ID` FOREIGN KEY (`product_id`) REFERENCES `catalog_product_entity` (`entity_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `SALES_BESTSELLERS_AGGREGATED_MONTHLY_STORE_ID_STORE_STORE_ID` FOREIGN KEY (`store_id`) REFERENCES `store` (`store_id`) ON DELETE CASCADE;

--
-- Constraints for table `sales_bestsellers_aggregated_yearly`
--
ALTER TABLE `sales_bestsellers_aggregated_yearly`
  ADD CONSTRAINT `SALES_BESTSELLERS_AGGRED_YEARLY_PRD_ID_CAT_PRD_ENTT_ENTT_ID` FOREIGN KEY (`product_id`) REFERENCES `catalog_product_entity` (`entity_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `SALES_BESTSELLERS_AGGREGATED_YEARLY_STORE_ID_STORE_STORE_ID` FOREIGN KEY (`store_id`) REFERENCES `store` (`store_id`) ON DELETE CASCADE;

--
-- Constraints for table `sales_creditmemo`
--
ALTER TABLE `sales_creditmemo`
  ADD CONSTRAINT `SALES_CREDITMEMO_ORDER_ID_SALES_ORDER_ENTITY_ID` FOREIGN KEY (`order_id`) REFERENCES `sales_order` (`entity_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `SALES_CREDITMEMO_STORE_ID_STORE_STORE_ID` FOREIGN KEY (`store_id`) REFERENCES `store` (`store_id`) ON DELETE SET NULL;

--
-- Constraints for table `sales_creditmemo_comment`
--
ALTER TABLE `sales_creditmemo_comment`
  ADD CONSTRAINT `SALES_CREDITMEMO_COMMENT_PARENT_ID_SALES_CREDITMEMO_ENTITY_ID` FOREIGN KEY (`parent_id`) REFERENCES `sales_creditmemo` (`entity_id`) ON DELETE CASCADE;

--
-- Constraints for table `sales_creditmemo_item`
--
ALTER TABLE `sales_creditmemo_item`
  ADD CONSTRAINT `SALES_CREDITMEMO_ITEM_PARENT_ID_SALES_CREDITMEMO_ENTITY_ID` FOREIGN KEY (`parent_id`) REFERENCES `sales_creditmemo` (`entity_id`) ON DELETE CASCADE;

--
-- Constraints for table `sales_invoice`
--
ALTER TABLE `sales_invoice`
  ADD CONSTRAINT `SALES_INVOICE_ORDER_ID_SALES_ORDER_ENTITY_ID` FOREIGN KEY (`order_id`) REFERENCES `sales_order` (`entity_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `SALES_INVOICE_STORE_ID_STORE_STORE_ID` FOREIGN KEY (`store_id`) REFERENCES `store` (`store_id`) ON DELETE SET NULL;

--
-- Constraints for table `sales_invoiced_aggregated`
--
ALTER TABLE `sales_invoiced_aggregated`
  ADD CONSTRAINT `SALES_INVOICED_AGGREGATED_STORE_ID_STORE_STORE_ID` FOREIGN KEY (`store_id`) REFERENCES `store` (`store_id`) ON DELETE SET NULL;

--
-- Constraints for table `sales_invoiced_aggregated_order`
--
ALTER TABLE `sales_invoiced_aggregated_order`
  ADD CONSTRAINT `SALES_INVOICED_AGGREGATED_ORDER_STORE_ID_STORE_STORE_ID` FOREIGN KEY (`store_id`) REFERENCES `store` (`store_id`) ON DELETE SET NULL;

--
-- Constraints for table `sales_invoice_comment`
--
ALTER TABLE `sales_invoice_comment`
  ADD CONSTRAINT `SALES_INVOICE_COMMENT_PARENT_ID_SALES_INVOICE_ENTITY_ID` FOREIGN KEY (`parent_id`) REFERENCES `sales_invoice` (`entity_id`) ON DELETE CASCADE;

--
-- Constraints for table `sales_invoice_item`
--
ALTER TABLE `sales_invoice_item`
  ADD CONSTRAINT `SALES_INVOICE_ITEM_PARENT_ID_SALES_INVOICE_ENTITY_ID` FOREIGN KEY (`parent_id`) REFERENCES `sales_invoice` (`entity_id`) ON DELETE CASCADE;

--
-- Constraints for table `sales_order`
--
ALTER TABLE `sales_order`
  ADD CONSTRAINT `SALES_ORDER_CUSTOMER_ID_CUSTOMER_ENTITY_ENTITY_ID` FOREIGN KEY (`customer_id`) REFERENCES `customer_entity` (`entity_id`) ON DELETE SET NULL,
  ADD CONSTRAINT `SALES_ORDER_STORE_ID_STORE_STORE_ID` FOREIGN KEY (`store_id`) REFERENCES `store` (`store_id`) ON DELETE SET NULL;

--
-- Constraints for table `sales_order_address`
--
ALTER TABLE `sales_order_address`
  ADD CONSTRAINT `SALES_ORDER_ADDRESS_PARENT_ID_SALES_ORDER_ENTITY_ID` FOREIGN KEY (`parent_id`) REFERENCES `sales_order` (`entity_id`) ON DELETE CASCADE;

--
-- Constraints for table `sales_order_aggregated_created`
--
ALTER TABLE `sales_order_aggregated_created`
  ADD CONSTRAINT `SALES_ORDER_AGGREGATED_CREATED_STORE_ID_STORE_STORE_ID` FOREIGN KEY (`store_id`) REFERENCES `store` (`store_id`) ON DELETE SET NULL;

--
-- Constraints for table `sales_order_aggregated_updated`
--
ALTER TABLE `sales_order_aggregated_updated`
  ADD CONSTRAINT `SALES_ORDER_AGGREGATED_UPDATED_STORE_ID_STORE_STORE_ID` FOREIGN KEY (`store_id`) REFERENCES `store` (`store_id`) ON DELETE SET NULL;

--
-- Constraints for table `sales_order_item`
--
ALTER TABLE `sales_order_item`
  ADD CONSTRAINT `SALES_ORDER_ITEM_ORDER_ID_SALES_ORDER_ENTITY_ID` FOREIGN KEY (`order_id`) REFERENCES `sales_order` (`entity_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `SALES_ORDER_ITEM_STORE_ID_STORE_STORE_ID` FOREIGN KEY (`store_id`) REFERENCES `store` (`store_id`) ON DELETE SET NULL;

--
-- Constraints for table `sales_order_payment`
--
ALTER TABLE `sales_order_payment`
  ADD CONSTRAINT `SALES_ORDER_PAYMENT_PARENT_ID_SALES_ORDER_ENTITY_ID` FOREIGN KEY (`parent_id`) REFERENCES `sales_order` (`entity_id`) ON DELETE CASCADE;

--
-- Constraints for table `sales_order_status_history`
--
ALTER TABLE `sales_order_status_history`
  ADD CONSTRAINT `SALES_ORDER_STATUS_HISTORY_PARENT_ID_SALES_ORDER_ENTITY_ID` FOREIGN KEY (`parent_id`) REFERENCES `sales_order` (`entity_id`) ON DELETE CASCADE;

--
-- Constraints for table `sales_order_status_label`
--
ALTER TABLE `sales_order_status_label`
  ADD CONSTRAINT `SALES_ORDER_STATUS_LABEL_STATUS_SALES_ORDER_STATUS_STATUS` FOREIGN KEY (`status`) REFERENCES `sales_order_status` (`status`) ON DELETE CASCADE,
  ADD CONSTRAINT `SALES_ORDER_STATUS_LABEL_STORE_ID_STORE_STORE_ID` FOREIGN KEY (`store_id`) REFERENCES `store` (`store_id`) ON DELETE CASCADE;

--
-- Constraints for table `sales_order_status_state`
--
ALTER TABLE `sales_order_status_state`
  ADD CONSTRAINT `SALES_ORDER_STATUS_STATE_STATUS_SALES_ORDER_STATUS_STATUS` FOREIGN KEY (`status`) REFERENCES `sales_order_status` (`status`) ON DELETE CASCADE;

--
-- Constraints for table `sales_order_tax_item`
--
ALTER TABLE `sales_order_tax_item`
  ADD CONSTRAINT `SALES_ORDER_TAX_ITEM_ASSOCIATED_ITEM_ID_SALES_ORDER_ITEM_ITEM_ID` FOREIGN KEY (`associated_item_id`) REFERENCES `sales_order_item` (`item_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `SALES_ORDER_TAX_ITEM_ITEM_ID_SALES_ORDER_ITEM_ITEM_ID` FOREIGN KEY (`item_id`) REFERENCES `sales_order_item` (`item_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `SALES_ORDER_TAX_ITEM_TAX_ID_SALES_ORDER_TAX_TAX_ID` FOREIGN KEY (`tax_id`) REFERENCES `sales_order_tax` (`tax_id`) ON DELETE CASCADE;

--
-- Constraints for table `sales_payment_transaction`
--
ALTER TABLE `sales_payment_transaction`
  ADD CONSTRAINT `FK_B99FF1A06402D725EBDB0F3A7ECD47A2` FOREIGN KEY (`parent_id`) REFERENCES `sales_payment_transaction` (`transaction_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `SALES_PAYMENT_TRANSACTION_ORDER_ID_SALES_ORDER_ENTITY_ID` FOREIGN KEY (`order_id`) REFERENCES `sales_order` (`entity_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `SALES_PAYMENT_TRANSACTION_PAYMENT_ID_SALES_ORDER_PAYMENT_ENTT_ID` FOREIGN KEY (`payment_id`) REFERENCES `sales_order_payment` (`entity_id`) ON DELETE CASCADE;

--
-- Constraints for table `sales_refunded_aggregated`
--
ALTER TABLE `sales_refunded_aggregated`
  ADD CONSTRAINT `SALES_REFUNDED_AGGREGATED_STORE_ID_STORE_STORE_ID` FOREIGN KEY (`store_id`) REFERENCES `store` (`store_id`) ON DELETE SET NULL;

--
-- Constraints for table `sales_refunded_aggregated_order`
--
ALTER TABLE `sales_refunded_aggregated_order`
  ADD CONSTRAINT `SALES_REFUNDED_AGGREGATED_ORDER_STORE_ID_STORE_STORE_ID` FOREIGN KEY (`store_id`) REFERENCES `store` (`store_id`) ON DELETE SET NULL;

--
-- Constraints for table `sales_sequence_profile`
--
ALTER TABLE `sales_sequence_profile`
  ADD CONSTRAINT `SALES_SEQUENCE_PROFILE_META_ID_SALES_SEQUENCE_META_META_ID` FOREIGN KEY (`meta_id`) REFERENCES `sales_sequence_meta` (`meta_id`) ON DELETE CASCADE;

--
-- Constraints for table `sales_shipment`
--
ALTER TABLE `sales_shipment`
  ADD CONSTRAINT `SALES_SHIPMENT_ORDER_ID_SALES_ORDER_ENTITY_ID` FOREIGN KEY (`order_id`) REFERENCES `sales_order` (`entity_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `SALES_SHIPMENT_STORE_ID_STORE_STORE_ID` FOREIGN KEY (`store_id`) REFERENCES `store` (`store_id`) ON DELETE SET NULL;

--
-- Constraints for table `sales_shipment_comment`
--
ALTER TABLE `sales_shipment_comment`
  ADD CONSTRAINT `SALES_SHIPMENT_COMMENT_PARENT_ID_SALES_SHIPMENT_ENTITY_ID` FOREIGN KEY (`parent_id`) REFERENCES `sales_shipment` (`entity_id`) ON DELETE CASCADE;

--
-- Constraints for table `sales_shipment_item`
--
ALTER TABLE `sales_shipment_item`
  ADD CONSTRAINT `SALES_SHIPMENT_ITEM_PARENT_ID_SALES_SHIPMENT_ENTITY_ID` FOREIGN KEY (`parent_id`) REFERENCES `sales_shipment` (`entity_id`) ON DELETE CASCADE;

--
-- Constraints for table `sales_shipment_track`
--
ALTER TABLE `sales_shipment_track`
  ADD CONSTRAINT `SALES_SHIPMENT_TRACK_PARENT_ID_SALES_SHIPMENT_ENTITY_ID` FOREIGN KEY (`parent_id`) REFERENCES `sales_shipment` (`entity_id`) ON DELETE CASCADE;

--
-- Constraints for table `sales_shipping_aggregated`
--
ALTER TABLE `sales_shipping_aggregated`
  ADD CONSTRAINT `SALES_SHIPPING_AGGREGATED_STORE_ID_STORE_STORE_ID` FOREIGN KEY (`store_id`) REFERENCES `store` (`store_id`) ON DELETE SET NULL;

--
-- Constraints for table `sales_shipping_aggregated_order`
--
ALTER TABLE `sales_shipping_aggregated_order`
  ADD CONSTRAINT `SALES_SHIPPING_AGGREGATED_ORDER_STORE_ID_STORE_STORE_ID` FOREIGN KEY (`store_id`) REFERENCES `store` (`store_id`) ON DELETE SET NULL;

--
-- Constraints for table `search_query`
--
ALTER TABLE `search_query`
  ADD CONSTRAINT `SEARCH_QUERY_STORE_ID_STORE_STORE_ID` FOREIGN KEY (`store_id`) REFERENCES `store` (`store_id`) ON DELETE CASCADE;

--
-- Constraints for table `sitemap`
--
ALTER TABLE `sitemap`
  ADD CONSTRAINT `SITEMAP_STORE_ID_STORE_STORE_ID` FOREIGN KEY (`store_id`) REFERENCES `store` (`store_id`) ON DELETE CASCADE;

--
-- Constraints for table `store`
--
ALTER TABLE `store`
  ADD CONSTRAINT `STORE_GROUP_ID_STORE_GROUP_GROUP_ID` FOREIGN KEY (`group_id`) REFERENCES `store_group` (`group_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `STORE_WEBSITE_ID_STORE_WEBSITE_WEBSITE_ID` FOREIGN KEY (`website_id`) REFERENCES `store_website` (`website_id`) ON DELETE CASCADE;

--
-- Constraints for table `store_group`
--
ALTER TABLE `store_group`
  ADD CONSTRAINT `STORE_GROUP_WEBSITE_ID_STORE_WEBSITE_WEBSITE_ID` FOREIGN KEY (`website_id`) REFERENCES `store_website` (`website_id`) ON DELETE CASCADE;

--
-- Constraints for table `tax_calculation`
--
ALTER TABLE `tax_calculation`
  ADD CONSTRAINT `TAX_CALCULATION_CUSTOMER_TAX_CLASS_ID_TAX_CLASS_CLASS_ID` FOREIGN KEY (`customer_tax_class_id`) REFERENCES `tax_class` (`class_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `TAX_CALCULATION_PRODUCT_TAX_CLASS_ID_TAX_CLASS_CLASS_ID` FOREIGN KEY (`product_tax_class_id`) REFERENCES `tax_class` (`class_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `TAX_CALC_TAX_CALC_RATE_ID_TAX_CALC_RATE_TAX_CALC_RATE_ID` FOREIGN KEY (`tax_calculation_rate_id`) REFERENCES `tax_calculation_rate` (`tax_calculation_rate_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `TAX_CALC_TAX_CALC_RULE_ID_TAX_CALC_RULE_TAX_CALC_RULE_ID` FOREIGN KEY (`tax_calculation_rule_id`) REFERENCES `tax_calculation_rule` (`tax_calculation_rule_id`) ON DELETE CASCADE;

--
-- Constraints for table `tax_calculation_rate_title`
--
ALTER TABLE `tax_calculation_rate_title`
  ADD CONSTRAINT `FK_37FB965F786AD5897BB3AE90470C42AB` FOREIGN KEY (`tax_calculation_rate_id`) REFERENCES `tax_calculation_rate` (`tax_calculation_rate_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `TAX_CALCULATION_RATE_TITLE_STORE_ID_STORE_STORE_ID` FOREIGN KEY (`store_id`) REFERENCES `store` (`store_id`) ON DELETE CASCADE;

--
-- Constraints for table `tax_order_aggregated_created`
--
ALTER TABLE `tax_order_aggregated_created`
  ADD CONSTRAINT `TAX_ORDER_AGGREGATED_CREATED_STORE_ID_STORE_STORE_ID` FOREIGN KEY (`store_id`) REFERENCES `store` (`store_id`) ON DELETE CASCADE;

--
-- Constraints for table `tax_order_aggregated_updated`
--
ALTER TABLE `tax_order_aggregated_updated`
  ADD CONSTRAINT `TAX_ORDER_AGGREGATED_UPDATED_STORE_ID_STORE_STORE_ID` FOREIGN KEY (`store_id`) REFERENCES `store` (`store_id`) ON DELETE CASCADE;

--
-- Constraints for table `theme_file`
--
ALTER TABLE `theme_file`
  ADD CONSTRAINT `THEME_FILE_THEME_ID_THEME_THEME_ID` FOREIGN KEY (`theme_id`) REFERENCES `theme` (`theme_id`) ON DELETE CASCADE;

--
-- Constraints for table `translation`
--
ALTER TABLE `translation`
  ADD CONSTRAINT `TRANSLATION_STORE_ID_STORE_STORE_ID` FOREIGN KEY (`store_id`) REFERENCES `store` (`store_id`) ON DELETE CASCADE;

--
-- Constraints for table `ui_bookmark`
--
ALTER TABLE `ui_bookmark`
  ADD CONSTRAINT `UI_BOOKMARK_USER_ID_ADMIN_USER_USER_ID` FOREIGN KEY (`user_id`) REFERENCES `admin_user` (`user_id`) ON DELETE CASCADE;

--
-- Constraints for table `variable_value`
--
ALTER TABLE `variable_value`
  ADD CONSTRAINT `VARIABLE_VALUE_STORE_ID_STORE_STORE_ID` FOREIGN KEY (`store_id`) REFERENCES `store` (`store_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `VARIABLE_VALUE_VARIABLE_ID_VARIABLE_VARIABLE_ID` FOREIGN KEY (`variable_id`) REFERENCES `variable` (`variable_id`) ON DELETE CASCADE;

--
-- Constraints for table `weee_tax`
--
ALTER TABLE `weee_tax`
  ADD CONSTRAINT `WEEE_TAX_ATTRIBUTE_ID_EAV_ATTRIBUTE_ATTRIBUTE_ID` FOREIGN KEY (`attribute_id`) REFERENCES `eav_attribute` (`attribute_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `WEEE_TAX_COUNTRY_DIRECTORY_COUNTRY_COUNTRY_ID` FOREIGN KEY (`country`) REFERENCES `directory_country` (`country_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `WEEE_TAX_ENTITY_ID_CATALOG_PRODUCT_ENTITY_ENTITY_ID` FOREIGN KEY (`entity_id`) REFERENCES `catalog_product_entity` (`entity_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `WEEE_TAX_WEBSITE_ID_STORE_WEBSITE_WEBSITE_ID` FOREIGN KEY (`website_id`) REFERENCES `store_website` (`website_id`) ON DELETE CASCADE;

--
-- Constraints for table `widget_instance`
--
ALTER TABLE `widget_instance`
  ADD CONSTRAINT `WIDGET_INSTANCE_THEME_ID_THEME_THEME_ID` FOREIGN KEY (`theme_id`) REFERENCES `theme` (`theme_id`) ON DELETE CASCADE;

--
-- Constraints for table `widget_instance_page`
--
ALTER TABLE `widget_instance_page`
  ADD CONSTRAINT `WIDGET_INSTANCE_PAGE_INSTANCE_ID_WIDGET_INSTANCE_INSTANCE_ID` FOREIGN KEY (`instance_id`) REFERENCES `widget_instance` (`instance_id`) ON DELETE CASCADE;

--
-- Constraints for table `widget_instance_page_layout`
--
ALTER TABLE `widget_instance_page_layout`
  ADD CONSTRAINT `WIDGET_INSTANCE_PAGE_LAYOUT_PAGE_ID_WIDGET_INSTANCE_PAGE_PAGE_ID` FOREIGN KEY (`page_id`) REFERENCES `widget_instance_page` (`page_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `WIDGET_INSTANCE_PAGE_LYT_LYT_UPDATE_ID_LYT_UPDATE_LYT_UPDATE_ID` FOREIGN KEY (`layout_update_id`) REFERENCES `layout_update` (`layout_update_id`) ON DELETE CASCADE;

--
-- Constraints for table `wishlist`
--
ALTER TABLE `wishlist`
  ADD CONSTRAINT `WISHLIST_CUSTOMER_ID_CUSTOMER_ENTITY_ENTITY_ID` FOREIGN KEY (`customer_id`) REFERENCES `customer_entity` (`entity_id`) ON DELETE CASCADE;

--
-- Constraints for table `wishlist_item`
--
ALTER TABLE `wishlist_item`
  ADD CONSTRAINT `WISHLIST_ITEM_PRODUCT_ID_CATALOG_PRODUCT_ENTITY_ENTITY_ID` FOREIGN KEY (`product_id`) REFERENCES `catalog_product_entity` (`entity_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `WISHLIST_ITEM_STORE_ID_STORE_STORE_ID` FOREIGN KEY (`store_id`) REFERENCES `store` (`store_id`) ON DELETE SET NULL,
  ADD CONSTRAINT `WISHLIST_ITEM_WISHLIST_ID_WISHLIST_WISHLIST_ID` FOREIGN KEY (`wishlist_id`) REFERENCES `wishlist` (`wishlist_id`) ON DELETE CASCADE;

--
-- Constraints for table `wishlist_item_option`
--
ALTER TABLE `wishlist_item_option`
  ADD CONSTRAINT `FK_A014B30B04B72DD0EAB3EECD779728D6` FOREIGN KEY (`wishlist_item_id`) REFERENCES `wishlist_item` (`wishlist_item_id`) ON DELETE CASCADE;

/*!40101 SET CHARACTER_SET_CLIENT=@OLD_CHARACTER_SET_CLIENT */;
/*!40101 SET CHARACTER_SET_RESULTS=@OLD_CHARACTER_SET_RESULTS */;
/*!40101 SET COLLATION_CONNECTION=@OLD_COLLATION_CONNECTION */;
```
CTER_SET_CLIENT=@OLD_CHARACTER_SET_CLIENT */;
/*!40101 SET CHARACTER_SET_RESULTS=@OLD_CHARACTER_SET_RESULTS */;
/*!40101 SET COLLATION_CONNECTION=@OLD_COLLATION_CONNECTION */;

```
