<script lang="ts">
  import {
    CheckIcon,
    ClaimIcon,
    CopyButton,
    DownloadIcon,
    IconLink,
    ProfileImagePlaceholder,
    Tooltip,
  } from 'components';
  import { makeDownloadable } from 'src/components/page/home/uploadHelpers';
  import type { BasicDraft, Claim, ClaimMap } from 'src/helpers';
  import { formatWebsite } from 'src/helpers/claims';
  import { useParams } from 'svelte-navigator';
  import './publicProfileView.scss';
  import { publicProfileViewTooltip } from './publicProfileViewHelper';

  export let claimsMap: ClaimMap;

  // Specially treat the basic profile.
  const basicClaim: Claim | false =
    claimsMap?.basic?.content && claimsMap.basic;
  const basicDraft = basicClaim?.draft as BasicDraft;
  const otherClaims: Array<Claim> = Object.values(claimsMap).filter(
    (x) => x.type !== 'basic' && x.content
  );
  const params = useParams();

  let isCredentialSourceDropdownOpen = false;
  $: shouldDisplayOriginalImage = true;
</script>

<div
  class="self-center w-full break-all p-6 fade-in rounded-xl bg-white dropshadow-default public-profile-container mb-4"
>
  {#if basicClaim}
    {#if !basicDraft.logo || !shouldDisplayOriginalImage}
      <ProfileImagePlaceholder />
    {:else}
      <img
        src={basicDraft.logo || ''}
        class="img-self"
        alt="profile-logo"
        on:error={() => {
          shouldDisplayOriginalImage = false;
        }}
      />
    {/if}
    <div class="text-2xl font-bold body mb-2 mt-4">
      {basicDraft.alias || ''}
    </div>
  {/if}

  {#if basicClaim}
    <!-- Specially treat basicClaim -->
    <a href={formatWebsite(basicDraft.website)} target="_blank">
      <div class="my-6">{basicDraft.website || ''}</div>
    </a>
    <div class="break-normal description-section">
      {basicDraft.description || ''}
    </div>
    <div class="mt-10 mb-4">
      <hr />
    </div>
  {/if}
  <h3 style="margin-top:20px;margin-bottom:10px">Other Credentials</h3>
  <div class="flex flex-row items-center mt-3">
    {#each Object.values(otherClaims) as claim}
      <ClaimIcon {claim} tooltip={publicProfileViewTooltip(claim)} />
    {/each}
  </div>
  <div class="mt-10 mb-4">
    <hr />
  </div>
  <div
    class="cursor-pointer font-semibold my-4"
    on:click={() =>
      (isCredentialSourceDropdownOpen = !isCredentialSourceDropdownOpen)}
  >
    View Credential Sources
  </div>
  {#if isCredentialSourceDropdownOpen}
    {#each Object.values(claimsMap).filter((x) => !!x.content) as claim}
      <div class="flex w-full justify-between items-center mb-1">
        <small class="text-gray-370">{claim.display.proof}</small>

        <Tooltip
          tooltip="Issued by {claim.content.issuer
            .replace('did:pkh:eth:', '')
            .replace('did:pkh:tz:', '')
            .replace('did:web:', '')}"
        >
          <CopyButton
            text={claim.content.issuer
              .replace('did:pkh:eth:', '')
              .replace('did:pkh:tz:', '')
              .replace('did:web:', '')}
            color="green"
            class="w-4 h-4"
            icon={CheckIcon}
          />
        </Tooltip>
      </div>

      <div class="flex w-full justify-between	mb-2">
        <div>{claim.display.display}</div>
        <IconLink
          class="block w-4 h-4"
          icon={DownloadIcon}
          href={makeDownloadable(claim.content || claim.preparedContent)}
          download={`${claim.display.display}.json`}
        />
      </div>
    {/each}
  {/if}
</div>
