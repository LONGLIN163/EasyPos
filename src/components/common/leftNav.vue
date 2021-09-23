<template>
    <div class="leftNav">
        <ul>
            <li>
                 <i class="fa fa-eur" aria-hidden="true"></i>
                 <div>Cashier</div>
            </li>
            <li>
                 <i class="fa fa-sitemap" aria-hidden="true"></i>
                 <div>Shops</div>
            </li>
            <li>
                 <i class="fa fa-shopping-bag" aria-hidden="true"></i>
                 <div>Articles</div>
            </li>
            <li>
                 <i class="fa fa-vcard"></i>
                 <div>VIP</div>
            </li>
            <li>
                 <i class="fa fa-calculator" aria-hidden="true"></i>
                 <div>Set</div>
            </li>
        </ul>
    </div>
</template>

<script>

export default {
    
}
</script>


<style>
    .leftNav{
        color:#fff;
        font-size: 10px;
        height: 100%;
        background-color: rgb(7, 162, 223);
        float: left;
        width: 5%;
    }
    .fa{
        font-size: 24px;
    } 
    .leftNav ul{
        padding: 0px;
        margin: 0px;
    }
    .leftNav li{
        list-style: none;
        text-align: center;
        border-bottom: 1px solid rgb(255, 255, 255);
        padding: 10px;
    }

</style>