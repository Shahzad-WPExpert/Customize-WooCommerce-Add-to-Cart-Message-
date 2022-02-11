# Customize-WooCommerce-Add-to-Cart-Message-
When the user Hit the Add to Cart button The message show "Product_Name has been added to your cart". 



/**
 * Change WooCommerce Add to cart message with cart link.
 */
function quadlayers_add_to_cart_message_html( $message, $products ) {

$count = 0;
$titles = array();
foreach ( $products as $product_id => $qty ) {
$titles[] = ( $qty > 1 ? absint( $qty ) . ' &times; ' : '' ) . sprintf( _x( '&ldquo;%s&rdquo;', 'Item name in quotes', 'woocommerce' ), strip_tags( get_the_title( $product_id ) ) );
$count += $qty;
}

$titles     = array_filter( $titles );
$added_text = sprintf( _n(
'%s has been added to your Cart.', // Singular
'%s have been added to your Cart.', // Plural
$count, // Number of products added
'woocommerce' // Textdomain
), wc_format_list_of_items( $titles ) );
$message    = sprintf( '<a href="%s" class="button wc-forward">%s</a> %s', esc_url( wc_get_page_permalink( 'cart' ) ), esc_html__( 'View Cart', 'woocommerce' ), esc_html( $added_text ) );

return $message;
}
add_filter( 'wc_add_to_cart_message_html', 'quadlayers_add_to_cart_message_html', 10, 2 );
