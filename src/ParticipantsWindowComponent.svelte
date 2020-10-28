<script>
    export let data;
    export let showHide;

    const mnpModalOpen = (link, e) => {
  	if (e) {
    	e.preventDefault();
    }
	window.top.radopen(link);
  	return false;
}
</script>

<div class="modal" data-shown={!showHide ? "0" : "1"}>
<span class="close">&times;</span>
  <div class="modal-content">
        <div class="user-cards">
            {#each data as item}
                <div class="mnp-list-item mnp-flex-y-center">
                    <div class="mnp-list-logo">
                        <img alt="" src="/GetAvatar.ashx?Id={item.userId}"/>
                    </div>
                    <div class="mnp-list-info">
                        <div class="mnp-nowrap">
                            <a href="/UserInfo.aspx?UserID={item.userId}" onclick="mnpModalOpen(this.href, event);" data-user-bd="{item.userId}">{item.fullName}</a>
                        </div>
                        <div class="mnp-list-subinfo">Подразделение: {item.department}</div>
                        <div class="mnp-list-subinfo">Должность: {item.position}</div>
                    </div>
                </div>
            {/each} 
        </div>
  </div>

</div>

<style>
    .user-cards {
        margin: 23px;
        display: grid;
        grid-template-columns: 1fr 1fr;
        grid-gap: 1vw;
    }
    
    .mnp-flex-y-center {
        align-items: center;
    }

    .mnp-list-item {
        display: flex;
        padding: 2px 10px;
        margin-top: 5px;
        box-shadow: 0 3px 6px rgba(0,0,0,0.16), 0 3px 6px rgba(0,0,0,0.23);
    }

    .mnp-list-logo {
        flex: 0 0 36px;
        width: 36px;
        height: 36px;
        overflow: hidden;
        border-radius: 50%;
        margin-right: 10px;
    }

    .mnp-list-logo img {
        object-fit: cover;
        width: 100%;
        height: 100%;
    }

    .mnp-list-info {
        flex: 1 1 auto;
        overflow: hidden;
        padding: 15px;
    }

    .mnp-nowrap { 
        white-space: nowrap;
        text-overflow: ellipsis;
        overflow: hidden;
    }

    .mnp-list-subinfo {
        font-size: 0.9rem;
        color: grey;
    }

    .modal {
    display: none; 
    position: fixed;
    z-index: 5;
    left: 0;
    top: 0;
    width: 100%; 
    height: 100%;
    overflow: auto;
    background-color: rgb(0,0,0);
    background-color: rgba(0,0,0,0.4);
    }

    .modal-content {
    background-color: #fefefe;
    margin: 15% auto;
    padding: 3px;
    border: 1px solid #888;
    width: 50%; 
    }

    .close {
    color: #fffbfb;
    float: right;
    font-size: 28px;
    font-weight: bold;
    padding-right: 15px;
    z-index: 1000;
    }

    .close:hover,
    .close:focus {
    color: black;
    text-decoration: none;
    cursor: pointer;
    }
</style>